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

wget -O $HOME/.stride/config/addrbook.json "https://github.com/mmc6185/node-testnets/blob/main/stride/addrbook.json?raw=true"
wget -qO $HOME/.stride/config/genesis.json "https://raw.githubusercontent.com/Stride-Labs/testnet/main/poolparty/genesis.json"

SEEDS="c0b278cbfb15674e1949e7e5ae51627cb2a2d0a9@seedv2.poolparty.stridenet.co:26656 (http://c0b278cbfb15674e1949e7e5ae51627cb2a2d0a9@seedv2.poolparty.stridenet.co:26656/)"
PEERS="d6583df382d418872ab5d71d45a1a8c3d28ff269@138.201.139.175:21016,05d7b774620b7afe28bba5fa9e002b436786d4c3@195.201.165.123:20086,d28cfff8b2fe03b597f67c96814fbfd19085b7c3@168.119.124.158:26656,a9687b78c13d39d2f96ec0905c6aa201671f61f0@78.107.234.44:25656,6922feb0ca2eab2be07d60fbfd275319bcd83ec9@77.244.66.222:26656,48b1310bc81deea3eb44173c5c26873c23565d33@34.135.129.186:26656,a3afae256ad780f873f85a0c377da5c8e9c28cb2@54.219.207.30:26656,dd93bd24192d8d3151264424e44b0f213d2334dc@162.55.173.64:26656,d46c3c3de3aacb7c75bbbbf1fe5c168f0c100f26@135.181.131.116:26683,c765007c489ddbcb80249579534e63d7a00407d0@65.108.225.158:22656"
sed -i -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.stride/config/config.toml

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" $HOME/.stride/config/config.toml
strided tendermint unsafe-reset-all --home $HOME/.stride
sudo systemctl start strided
journalctl -fu strided -o cat
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

<h1 align="center"> Peer sorunu yaşarsanız tek komutta </h1>

### YUKARDA SORUN ALMAZSANIZ YAPMAYIN SIFIRDAN BAŞLARSINIZ.


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

## Explorer kontrol: [Explorer Linki](https://stride.explorers.guru/)

## sorular için: https://t.me/StrideTurkish

# Discorddan role-requestten rol de alabılırsınız.

# Hesaplar:

[<img src="https://cdn-icons-png.flaticon.com/512/733/733579.png" width="16px"> Twitter   ](https://twitter.com/Ruesandora0) 

[<img src="https://cdn-icons-png.flaticon.com/512/1336/1336494.png" width="16px"> Forum   ](https://forum.rues.info/index.php)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Announcement   ](https://t.me/RuesAnnouncement)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Chat   ](https://t.me/+-l6GpqiNOxFiMTVk)

[Discord](https://discord.gg/ruescommunity)
