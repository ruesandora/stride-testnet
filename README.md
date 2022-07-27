<h1 align="center">Stride - Poll Party! </h1>

### Selamlar bugün Stride node testnetine katılacağız. SORULAR İÇİN: [Stride Türkiye](https://t.me/StrideTurkish)

![image](https://user-images.githubusercontent.com/101149671/180230551-dbc0d5f0-b087-483f-9e7a-95711a820209.png)


# Sistem gereksinimleri, "benim" önerim, CPU-RAM kısmında ekibin önerisi daha yüksek:

```
4 CPU
8 RAM
160 GB SSD
```

<h1 align="center"> SIFIRDAN KURULUM YAPACAKLAR İÇİN </h1>

## Kurulum:

```
wget -q -O stride.sh https://api.rues.info/stride.sh && chmod +x stride.sh && sudo /bin/bash stride.sh
```

## Cüzdan oluşturma: (not edin kaydedin)
```
strided keys add <walletName>
```

## Discordan test tokeni alma: [Discord Linki](https://discord.gg/4B4cbvCh)

![image](https://user-images.githubusercontent.com/101149671/180231116-4eaae21a-184c-4204-a3f1-e7ac945e1455.png)

## Validator oluşturma:

* MONİKER ve FROM kısımlarını düzenleyin.

```
strided tx staking create-validator \
--amount=9900000ustrd \
--pubkey=$(strided tendermint show-validator) \
--moniker=RuesValidator \
--chain-id=STRIDE-TESTNET-2 \
--commission-rate="0.10" \
--commission-max-rate="0.20" \
--commission-max-change-rate="0.1" \
--min-self-delegation="1" \
--fees=250ustrd \
--gas=200000 \
--from=rues \
--website="http://forum.rues.info/" \
--details="https://linktr.ee/ruesandora0" \
-y
```

<h1 align="center"> DAHA ÖNCE VALİDATOR OLUŞTURANLAR İÇİN </h1>


## Tek kalemde hepsini kopyalayıp terminale yapıştırın:
```
sudo systemctl stop strided
cd $HOME && rm -rf stride
git clone https://github.com/Stride-Labs/stride.git
cd stride
git checkout 3cb77a79f74e0b797df5611674c3fbd000dfeaa1
make build
sudo cp $HOME/stride/build/strided /usr/local/bin
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" $HOME/.stride/config/config.toml
strided tendermint unsafe-reset-all --home $HOME/.stride

SEEDS=""; \
PEERS="48b1310bc81deea3eb44173c5c26873c23565d33@34.135.129.186:26656,0f45eac9af97f4b60d12fcd9e14a114f0c085491@stride-library.poolparty.stridenet.co:26656 (http://,0f45eac9af97f4b60d12fcd9e14a114f0c085491@stride-library.poolparty.stridenet.co:26656/)"; \
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.stride/config/config.toml
wget -O $HOME/.stride/config/addrbook.json "https://github.com/mmc6185/node-testnets/blob/main/stride/addrbook.json?raw=true"
SNAP_RPC=https://stride-library.poolparty.stridenet.co:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.stride/config/config.toml
sudo systemctl restart strided && journalctl -u strided -f -o cat
```

## Eşleştikten sonra Validator oluşturun:

* MONİKER ve FROM kısımlarını düzenleyin.

```
strided tx staking create-validator \
--amount=9900000ustrd \
--pubkey=$(strided tendermint show-validator) \
--moniker=RuesValidator \
--chain-id=STRIDE-TESTNET-2 \
--commission-rate="0.10" \
--commission-max-rate="0.20" \
--commission-max-change-rate="0.1" \
--min-self-delegation="1" \
--fees=250ustrd \
--gas=200000 \
--from=rues \
--website="http://forum.rues.info/" \
--details="https://linktr.ee/ruesandora0" \
-y
```

## Peer sorunu yaşarsanız tek komutta:
```
cd
sudo systemctl stop strided
strided tendermint unsafe-reset-all --home $HOME/.stride
rm -rf $HOME/stride $HOME/go/bin/strided $HOME/.stride/config/genesis.json
git clone https://github.com/Stride-Labs/stride.git
cd stride
git checkout 644c7574ee79128970a81cf8b9f23351dcdeec62
mkdir -p $HOME/go/bin
make build 
wget -O $HOME/.stride/config/addrbook.json "https://github.com/mmc6185/node-testnets/blob/main/stride/addrbook.json?raw=true"
wget -O $HOME/.stride/config/genesis.json "https://raw.githubusercontent.com/Stride-Labs/testnet/main/poolparty/genesis.json"
sudo systemctl restart strided && journalctl -u strided -f -o cat

State sync komutları :
sudo systemctl stop strided
strided tendermint unsafe-reset-all --home $HOME/.stride
SEEDS=""; \
PEERS="48b1310bc81deea3eb44173c5c26873c23565d33@34.135.129.186:26656,0f45eac9af97f4b60d12fcd9e14a114f0c085491@stride-library.poolparty.stridenet.co:26656"; \
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.stride/config/config.toml
wget -O $HOME/.stride/config/addrbook.json "https://raw.githubusercontent.com/StakeTake/guidecosmos/main/stride/STRIDE-TESTNET-2/addrbook.json"
SNAP_RPC=https://stride-library.poolparty.stridenet.co:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.stride/config/config.toml
sudo systemctl restart strided && journalctl -u strided -f -o cat
```

## Explorer kontrol: [Explorer Linki](https://stride.explorers.guru/)

## sorular için: https://t.me/StrideTurkish

# Discorddan role-requestten rol de alabılırsınız.

# Hesaplar:

[<img src="https://cdn-icons-png.flaticon.com/512/733/733579.png" width="16px"> Twitter   ](https://twitter.com/Ruesandora0) 

[<img src="https://cdn-icons-png.flaticon.com/512/1336/1336494.png" width="16px"> Forum   ](https://forum.rues.info/index.php)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Announcement   ](https://t.me/RuesAnnouncement)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Chat   ](https://t.me/+-l6GpqiNOxFiMTVk)

[Discord](https://discord.gg/ruescommunity)
