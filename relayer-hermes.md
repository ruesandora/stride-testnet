<h1 align="center"> FLOOD TAMAMLANMADI KURULUM YAPMAYIN </h1>



<h1 align="center">Selamlar, bugün Stride görevlerini  yapıp form dolduracağız, floodu detaylı okuyunuz, çünkü ELENME durumu söz konusu </h1>

# Bazı görevlerde yalnızsınız, kişisel görevler, ben açıklama bırakacağım sizin yapmanız gerekiyor, "ANCAK":

* Kişisel görevlerde başkasının görevini veya PR'ını (pull request) kopyalamak veya discord/telegram kanallarında sormak yasak.
* Sadece #incentive-tasks discord odasında sorabilirsiniz görev sorularını.
* Görevleri merak ediyorsanız: [Görev Listesi](https://github.com/Stride-Labs/testnet/tree/main/incentivized-testnet)
* Bunlar dışında sorunuz varsa: [Stride Türkiye](https://t.me/StrideTurkish)
* Görev formu, her görev için 1 form doldurulacak [Form](https://docs.google.com/forms/d/e/1FAIpQLSeoZEC5kd89KCQSJjn5Zpf-NQPX-Gc8ERjTIChK1BEbiVfMVQ/viewform)

<h1 align="center">Paylaşabileceğim görevlerin rehberi: </h1>

# Likidite - Staking görevi: 

* ÖNEMLİ: Altta yapacağınız işlemlerin hepsini TX'ini alıp explorerde aratın, succes olmuşsa TX'i kaydedin. [Explorer](https://poolparty.stride.zone/STRIDE)
* Cüzdan adınızı ekleyin.

```
strided tx stakeibc liquid-stake 1000 uatom --from CÜZDAN ADINIZ --chain-id STRIDE-TESTNET-2 --gas auto -y
```

# Redeem görevi:

* Cosmos: cüzdanı kısmına KEPLR'da yazan GAIA ağını ekleyın.
* From: kısmı cüzdan adınız
* GAIA ağını eklemek için : https://twitter.com/Ruesandora0/status/1550485313243545601?s=20&t=PWfmmnIxju9LN-kGW5VznA

```
strided tx stakeibc redeem-stake 500 GAIA cosmos1vm6wnmvxugqj8k6s6d2cktgctc550qaq50kyye  --chain-id STRIDE-TESTNET-2 --from CÜZDANADIN --gas 500000 -y
```

# Claim görevi:

* Şu an burada claim edilcek token gözükmüyor, hata alabilir herkes, bende aldım. İsterseniz deneyin, düzelirse paylaşırım telegramda

```
strided tx stakeibc claim-undelegated-tokens GAIA 296 stride1d6v2gd0hzzg8hp7jzkfsp8uyqd5hh5tsnvjxuv --chain-id STRIDE-TESTNET-2 --from rues -y
```

## Bu üçü tek göreve karşılık geliyor (6 numaralı görev)

![image](https://user-images.githubusercontent.com/101149671/183288571-5c78da8f-f01d-412a-922e-0b18b66c7751.png)


# IBC, bu, görevler arasında yok ama neden yapmayalım :):

* From cüzdan adınız olcak.
* Komutu direkt kullanabilirsiniz

```
strided tx ibc-transfer -y transfer transfer channel-22 sei1654kj35pszp4t49wcglwcg0cwlxg5vvw8rv32t 10000ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2  --chain-id STRIDE-TESTNET-2 --from rues
```

## Kolay görevler:

* 7 gün validator çalıştırmak (validator linki verırsınız forma)
* Discordda 20 kişinin sorusunu cevaplamak

<h1 align="center">LÜTFEN BURAYI ÇOK DİKKATLİ OKUYUN, ÖDÜL HAKKINIZI KAYBETMEYİN </h1>

# Relayer görevi hakkında:

### Arkadaşlar normal şartlarda buraları kendiniz yapmanız gerekiyor, benim paylaşmamam gerekiyor, bunu yapmama müsade edilmiyor, herkesin kendisi yapılması konusunda ısrarla belirtilmiş, yaklaşık 4 gündür bu konu ile ilgileniyorum.. Lütfen unutmayın bu sorular "TELEGRAMDA" veya "DİSCORDDA" sormanız yasak.. Stride Türkiye grubunun Resmi kanal olduğunu unutmayın, burada yalnızsınız ve sizin gayretinize kalmış. (Normalde bir sürü şey yazmıştım ama buna izin yokmuş :/)

### AMA size rehber olması açısından bir şeyler göstereceğim, sorular için sadece discordu kullanabılıyorsunuz relay 2 için

![image](https://user-images.githubusercontent.com/101149671/183241967-5b0cddee-df42-4722-a372-974e8ad1369d.png)

### Gördüğünüz gibi günlerdir bu dertle uğraşıyorum, tamamen yalnızsınız, telegramda sormayın (telegram bana ait değil resmi Türkiye orası):

![image](https://user-images.githubusercontent.com/101149671/183242178-3a251579-6cca-4e4f-bbc8-d096bc2c2c0e.png)

<h1 align="center"> HERMES </h1>

# GAIA:

* NOT: Dün Sei ile hermes'i göstermiştim ancak bir çok kişi hata alıyor bundan dolayı şu an GAIA ile gösteriyorum.

* NOT: GAIA'nız yoksa ilk başta GAIA kuralım.

* NOT: İster aynı sunucuya ister farklı sunucuya.. Benim sunucumda 20-30 GB yer kapladı.

* NOT: Düşük bir sunucunuz varsa farklı sunucuya kurun.

* NOT: Ben gaia kurmak ıstemıyorum var olan nodelara kurmak istiyorsanız SEİ-STRIDE hermes floodu dün yazmıştım [buradan](https://github.com/ruesandora/stride-testnet/blob/main/stride-sei-hermes.md) bulabilirsiniz.

* EN ÖNEMLİ NOT: Ekip GAIA istiyor.

## Validator adımızı düzenleyelim:
```
NODENAME=RuesValidator
```

## Değişkenleri kaydedelim:
```
GAIA_PORT=23
echo "export NODENAME=$NODENAME" >> $HOME/.bash_profile
if [ ! $WALLET ]; then
	echo "export WALLET=wallet" >> $HOME/.bash_profile
fi
echo "export GAIA_CHAIN_ID=GAIA" >> $HOME/.bash_profile
echo "export GAIA_PORT=${GAIA_PORT}" >> $HOME/.bash_profile
source $HOME/.bash_profile
```
## Güncellemeler:
```
sudo apt update && sudo apt upgrade -y
```
```
sudo apt install curl build-essential git wget jq make gcc tmux chrony -y
```

## Go kurulumu:

* Not: go kurdunuz mu kurmadınız mı bılmıyorum belki sıfır sunucuya kuruyorsunuz GAIA'yı. `go version` ile kontrol edebilirsiniz.

```
if ! [ -x "$(command -v go)" ]; then
  ver="1.18.2"
  cd $HOME
  wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
  sudo rm -rf /usr/local/go
  sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
  rm "go$ver.linux-amd64.tar.gz"
  echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile
  source ~/.bash_profile
fi
```

## Binary:
```
cd $HOME
git clone https://github.com/Stride-Labs/gaia.git
cd gaia
git checkout 5b47714dd5607993a1a91f2b06a6d92cbb504721
make build
sudo cp $HOME/gaia/build/gaiad /usr/local/bin
```

## config
```
gaiad config chain-id $GAIA_CHAIN_ID
gaiad config keyring-backend test
gaiad config node tcp://localhost:${GAIA_PORT}657
```

## İnit:
```
gaiad init $NODENAME --chain-id $GAIA_CHAIN_ID
```

## genesis:
```
wget -qO $HOME/.gaia/config/genesis.json "https://raw.githubusercontent.com/Stride-Labs/testnet/main/poolparty/gaia/gaia_genesis.json"
```

## Seed ve peerler ve bağlantılar:
```
SEEDS=""
PEERS="ec829f12f6d513384e6c5ae79220455e0d80163c@104.208.67.175:23656,88f9b658a77a1ed7376adbc6d0584da8c1a35f6f@176.124.213.56:23656,b8948a13a8953f864ff43fa31ede14a21e44efdc@88.208.57.200:26656,b3dee7da18fc03c8f9481bad25a06138c7badd8c@86.48.2.74:23656,b7716bc446bd0c636ccb343c408065af71fbb576@159.65.20.94:23656,4f0e774fdf629771045fc95e74145d04e899af92@134.122.96.36:23656,a3720d1999a88056ef74fdb923e27dfd9c24c01d@40.114.118.113:23656,8f7058c8d3ba5b889c9895ed4525cb89e64f0a8b@75.119.133.19:23656,b767515dca0be232fc287e0d274831a8c80fcac7@5.9.147.22:26256,c3c32094135bc9d9148dbcbac52fdace8d01d62c@51.77.108.119:23656,a3b3668f967de210ae31ce779deed03f91074038@185.249.225.35:23656,d241b443f87c613d8e7039acd64ff7c296166b99@38.242.134.205:23656,8e2cf0c23b69924a8442b8102951778bd5254773@38.242.233.25:23656,4e6ba3223ba24e27eccffede205e4cffcbae903a@38.242.135.66:23656,9c86d46e33566001c89d274e2559932a4e98e406@20.90.88.145:23656,ccadfbc7c6204887edc9a6eba5f9beed78ffe9de@149.102.137.76:23656,c24fecd05c85385aaa84e587557285e7dfe38d54@217.160.207.56:23656,c6dcce40e8b8a00f353a642ef0ee3623a333c067@20.230.133.117:23656,964f3d7398196238acd9e26cc96ad7787c7513f6@45.130.104.89:23656,ff3a2a2022b2d53541efc0403af302eae2775da5@51.159.182.149:23656,6567e116f975eb36be8e15598f10917dab831c35@31.207.44.66:23656,853174f1ca8b78fbbfdefd32af7cc1f3fc424ce3@185.182.187.33:23656,6fd97df135f806249b55789d314b1482df38d366@20.213.53.251:23656,2101d45204248d9a8b825a23950370029d5e136e@195.88.87.43:23656,75c0154117e46f29b1eee482d740f0cc73ef76ed@164.92.80.118:23656,f6149bcd125f8972b0dc333c84cfef6fc3b9b54a@20.193.154.140:23656,6b85c6a0b2cdcf05d0ce5b2f6a78728b510fcb01@131.255.179.4:23656,87c1cebe140dbde04644e62a31af7863fa1b4fc5@157.245.0.168:23656,a64faaf6fe45425352524341d2f390ce6c603c09@139.162.2.113:23656,712f37d4e5f080452759bb6f4c7ed1716270584f@20.25.144.37:23656,23e60781c1e71968d7412cb6f45aa7d5648f2517@52.234.146.133:23656,aa3aa0e1244c0503b6d94d7a2ab4554ba0e3fd79@173.212.233.187:23656,7f248115c0636860cfcdfaec5a20f42bc6d622a2@38.242.222.136:23656"
sed -i -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.gaia/config/config.toml
```

```
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:${GAIA_PORT}658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:${GAIA_PORT}657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:${GAIA_PORT}060\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:${GAIA_PORT}656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":${GAIA_PORT}660\"%" $HOME/.gaia/config/config.toml
sed -i.bak -e "s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:${GAIA_PORT}317\"%; s%^address = \":8080\"%address = \":${GAIA_PORT}080\"%; s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:${GAIA_PORT}090\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:${GAIA_PORT}091\"%" $HOME/.gaia/config/app.toml
```

## Pruning (bence yapın yer kaplamasın)
```
pruning="custom"
pruning_keep_recent="100"
pruning_keep_every="0"
pruning_interval="50"
sed -i -e "s/^pruning *=.*/pruning = \"$pruning\"/" $HOME/.gaia/config/app.toml
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"$pruning_keep_recent\"/" $HOME/.gaia/config/app.toml
sed -i -e "s/^pruning-keep-every *=.*/pruning-keep-every = \"$pruning_keep_every\"/" $HOME/.gaia/config/app.toml
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"$pruning_interval\"/" $HOME/.gaia/config/app.toml
```

## Gerekli ayarlar:
```
sed -i -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0uatom\"/" $HOME/.gaia/config/app.toml
```
```
sed -i -e "s/prometheus = false/prometheus = true/" $HOME/.gaia/config/config.toml
```
```
gaiad tendermint unsafe-reset-all --home $HOME/.gaia
```

## Servis dosyası:
```
sudo tee /etc/systemd/system/gaiad.service > /dev/null <<EOF
[Unit]
Description=gaia
After=network-online.target

[Service]
User=$USER
ExecStart=$(which gaiad) start --home $HOME/.gaia
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```

## Başlatalım:
```
sudo systemctl daemon-reload
sudo systemctl enable gaiad
sudo systemctl restart gaiad && sudo journalctl -u gaiad -f -o cat
```

## Hızlı eşleşmek için state sync:

* Burası 5 dakikada sürebilir 1 saatte, talebe bağlı.

```
SNAP_RPC1="https://gaia.poolparty.stridenet.co:445" \
&& SNAP_RPC2="https://gaia.poolparty.stridenet.co:445"
LATEST_HEIGHT=$(curl -s $SNAP_RPC2/block | jq -r .result.block.header.height) \
&& BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)) \
&& TRUST_HASH=$(curl -s "$SNAP_RPC2/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC1,$SNAP_RPC2\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.gaia/config/config.toml
gaiad tendermint unsafe-reset-all --home $HOME/.gaia
sudo systemctl restart gaiad && journalctl -fu gaiad -o cat
```

## Eşleşirken cüzdan

* Cüzdan oluşturduktan sonra [faucettan](https://discord.gg/3XSNGPDN) ATOM alın.

* İster yeni oluşturun:
```
gaiad keys add $WALLET
```

* İsterseniz Stride cüzdanınızı kullanın:
```
gaiad keys add $WALLET --recover
```

## Validator oluşturun ve explorerden kontrol edin.

* Eşleşmeden validator oluşturmayın
* [Explorer Link](https://poolparty.stride.zone/GAIA/staking)

```
gaiad tx staking create-validator \
  --amount 1000000uatom \
  --from Rues \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(gaiad tendermint show-validator) \
  --moniker RuesValidator \
  --chain-id GAIA
```

<h1 align="center"> STRIDE-GAIA HERMES </h1>

# Bu rehber, Hermes'i Stride STRIDE-TESTNET-2 nodeunuzun kurulu olduğu sunucu ile aynı sunucuya kurulum yapacağınızı varsayar ve yapılandırmalar ona göre ayarlanmıştır. 

## BU KISIM STRIDE ICERSINDE CALISTIRILACAK

*  `hermes version` yazdığınızda hermes 0.15.0+4e83aae diye çıktı alırsınız.

```
sudo apt install unzip
wget https://github.com/informalsystems/ibc-rs/releases/download/v0.15.0/hermes-v0.15.0-x86_64-unknown-linux-gnu.zip
unzip hermes-v0.15.0-x86_64-unknown-linux-gnu.zip
sudo mv hermes /usr/bin

mkdir -p $HOME/hermes
mkdir -p $HOME/.hermes
mkdir -p $HOME/.hermes/keys

hermes version
```

## Değişkenleri ayarlayın:

* Bu kısım sadece GAIA node içinde çalıştırılacak
* Bu kısım sadece GAIA node içinde çalıştırılacak
* Bu kısım sadece GAIA node içinde çalıştırılacak

```
PORTN=$(grep -A 3 "\[p2p\]" ~/.gaia/config/config.toml | egrep -o ":[0-9]+")
sed -i.bak 's/external_address = ""/external_address = "'"$(curl -4 ifconfig.co)"''$PORTN'"/g' $HOME/.gaia/config/config.toml

PORTR=$(grep -A 3 "\[rpc\]" ~/.gaia/config/config.toml | egrep -o ":[0-9]+")
sed -i.bak -e "s%^laddr = \"tcp://127.0.0.1$PORTR\"%laddr = \"tcp://0.0.0.0$PORTR\"%" $HOME/.gaia/config/config.toml
sed -i.bak -e "s/indexer *=.*/indexer = \"kv\"/g" $HOME/.gaia/config/config.toml

systemctl restart gaiad
```

## GRPC bilgisi alıyoruz:

* `165.227.165.197:23090` bu şekilde bir port çıktısı olacak
* Herkeste aynı port olmaz
* Not edin

```
echo "$(curl -s ifconfig.me)$(grep -A 6 "\[grpc\]" ~/.gaia/config/app.toml | egrep -o ":[0-9]+")"
```

## RPC bilgisi alıyoruz

* `165.227.165.197:23657` bu şekilde bir port çıktısı olacak
* Herkeste aynı port olmaz
* Not edin

```
echo "$(curl -s ifconfig.me)$(grep -A 3 "\[rpc\]" ~/.gaia/config/config.toml | egrep -o ":[0-9]+")"
```

# BUNDAN SONRAKİLER STRIDE NODU İÇERSİNDE SADECE

* Yukarda aldığımız port+IP bilgilerini tırnak içersine girelim:
* Örnek: GRPC="165.227.165.197:23090"
* Birinci GRPC ikinci RPC

```
GRPC=""
RPC=""
```

## Mnemonicleri girelim:

* Mnemonic = 24 kelime
* Tırnak içersine mnemonicleri girin.
* mnemonic 1 STRIDE, mnemonic 2 GAIA
* Aynı cüzdanı/mnemonic kullandıysanız aynı olacak..

```
MNEMONIC1=""
MNEMONIC2=""
```

## Hermes'de özel bir imzamız olsun istemez miyiz?

* Discord adına kendi discord ID'inizi girin.

```
MEMO="RuesCommunity|! Rues#9144 "
```

## Şimdi, bu komutları çalıştırın:
```
sed -i.bak 's/external_address = ""/external_address = "'"$(curl -4 ifconfig.co)"':26656"/g' $HOME/.stride/config/config.toml
PORTR=$(grep -A 3 "\[rpc\]" ~/.stride/config/config.toml | egrep -o ":[0-9]+")
PORTG=$(grep -A 6 "\[grpc\]" ~/.stride/config/app.toml | egrep -o ":[0-9]+")
```

## TEK SEFERDE Terminalde Çalıştırın
```
sudo tee $HOME/.hermes/config.toml > /dev/null <<EOF
[global]
log_level = 'info'

[mode]

[mode.clients]
enabled = true
refresh = true
misbehaviour = true

[mode.connections]
enabled = false

[mode.channels]
enabled = false

[mode.packets]
enabled = true
clear_interval = 100
clear_on_start = true
tx_confirmation = true

[rest]
enabled = false
host = '127.0.0.1'
port = 3000

[telemetry]
enabled = false
host = '127.0.0.1'
port = 3001

[[chains]]
id = 'STRIDE-TESTNET-2'
rpc_addr = 'http://127.0.0.1$PORTR'
grpc_addr = 'http://127.0.0.1$PORTG'
websocket_addr = 'ws://127.0.0.1$PORTR/websocket'
rpc_timeout = '10s'
account_prefix = 'stride'
key_name = 'stride'
address_type = { derivation = 'cosmos' }
store_prefix = 'ibc'
default_gas = 100000
max_gas = 20000000
gas_price = { price = 0.001, denom = 'ustrd' }
gas_adjustment = 0.1
max_msg_num = 15
max_tx_size = 100000
clock_drift = '5s'
max_block_time = '30s'
trusting_period = '5hours'
memo_prefix = '$MEMO'
trust_threshold = { numerator = '1', denominator = '3' }

[[chains]]
id = 'GAIA'
rpc_addr = 'http://$RPC'
grpc_addr = 'http://$GRPC'
websocket_addr = 'ws://$RPC/websocket'
rpc_timeout = '10s'
account_prefix = 'cosmos'
key_name = 'test'
address_type = { derivation = 'cosmos' }
store_prefix = 'ibc'
default_gas = 300000
max_gas = 15000000
gas_price = { price = 0.000001, denom = 'uatom' }
gas_adjustment = 0.1
max_msg_num = 15
max_tx_size = 100000
clock_drift = '5s'
max_block_time = '30s'
trusting_period = '5hours'
memo_prefix = '$MEMO'
trust_threshold = { numerator = '1', denominator = '3' }
EOF
```

## Cüzdanınızı içe aktarın
```
hermes keys restore STRIDE-TESTNET-2 -m "$MNEMONIC1"
```
```
hermes keys restore GAIA -m "$MNEMONIC2"
```

## Hermes için daemon oluşturun
```
sudo tee /etc/systemd/system/hermesd.service > /dev/null <<EOF
[Unit]
Description=hermes

[Service]
User=$USER
ExecStart=/usr/bin/hermes start
LimitNOFILE=180000

Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
EOF
```

## Hermes Servisi başlatın
```
systemctl daemon-reload
systemctl enable hermesd
systemctl start hermesd
```

## Yapılandırmayı kontrol edin

* Çıktı da şunları görmelisiniz (ikisinden birisi yazar)

* Success: "validation passed successfully"
* Success: "configuration is valid"

```
hermes config validate
```

## Hermesin doğru çalışıp çalışmadığını kontrol edin
```
hermes health-check
```
![image](https://user-images.githubusercontent.com/101149671/183289390-93944929-c99f-47a8-8073-618c12d5f64d.png)

## Bu kısımda screen oluşturalım
```
apt-get install screen
```
```
screen -S hermes
```

## Logları kontrol edelim:
```
journalctl -u hermesd.service -fo cat
```

## Aşağıdaki komut hermes transfer komutu:

* Cüzdan adreslerinizi değiştirin.

```
hermes tx raw ft-transfer GAIA STRIDE-TESTNET-2 transfer channel-0 1000 -d ustrd -r strıdecüzdanı -t 60 -o 100
```
```
hermes tx raw ft-transfer STRIDE-TESTNET-2 GAIA transfer channel-0 1000 -d uatom -r gaıacüzdanı -t 60 -o 100
```

## Explorer'dan işlemleri kontrol edelim: [Explorer Linki](https://poolparty.stride.zone/GAIA/staking)

* tx hash'a tıklıyoruz:

![image](https://user-images.githubusercontent.com/101149671/183289537-8b1f65ae-4ea1-4fa5-ba46-74abd9e2e5f5.png)

* Yukarıda hatırlarsınız memo (imza) eklemiştik:

![image](https://user-images.githubusercontent.com/101149671/183290069-ea2bdf10-a1d1-4b6e-a308-2797f9f1f04f.png)


<h1 align="center"> RELAYER v2 </h1>


## BU KISIM STRIDE ICERSINDE CALISTIRILACAK

* INDEXER açma, hem STRIDE hemde GAIA için.. Hermesi yukardan GAIA-STRIDE ile kuranlar bu komutu atlasın.

* STRIDE (node içinde)
```
sed -i -e "s/^indexer *=.*/indexer = \"kv\"/" $HOME/.stride/config/config.toml
```

* GAIA (node içinde)
```
sed -i -e "s/^indexer *=.*/indexer = \"kv\"/" $HOME/.gaia/config/config.toml
```

## Değişkenleri ayarla

* Hermes'te ki gibi imza oluşturalım:
* Burayı not alın

```
RELAYER_ID='RuesCommunity|! Rues#9144' 
```

## Bu işlem Stride sunucu içince yapılacak..

* Burada config.toml'un içine girip, içinde ki RPC `127.0.0.1:16657` benzeri IP+port numaramızı alacağız.

```
nano $HOME/.stride/config/config.toml
```

## Yukarıda aldığımız ıp+port numarasını strıde_rpc_addr ve strıde mnemonicleri tırnak içersine giriyoruz.

* Bu bilgileri not ediniz.

```
STRIDE_RPC_ADDR='' 
STRIDE_MNEMONIC=''
```

![image](https://user-images.githubusercontent.com/101149671/183385825-cfbb2449-91f2-4b8b-bd17-9a14a0ccf959.png)

## Bu işlem GAIA sunucu içince yapılacak..

* Altta ki komutu girin ve çıktıyı 
* ıp+port numarasını gaıa_rpc_addr ve gaıa mnemonicleri tırnak içersine giriyoruz
* yukarıda yaptığımız gibi.

```
echo "$(curl -s ifconfig.me)$(grep -A 3 "\[rpc\]" ~/.gaia/config/config.toml | egrep -o ":[0-9]+")"
```
```
GAIA_RPC_ADDR='' 
GAIA_MNEMONIC=''
```

# Kurulum yapıyoruz, bundan sonraki TÜM İŞLEMLER STRIDE NODE İÇERSİNDE

* Yukarıda kaydettiğimiz değerleri tırnakların içersini doldurarak giriyoruz. 
* Sakın boş bırakmayın.
* Üçüncü komutta imzanıza discord adınızı girin.
```
STRIDE_RPC_ADDR='' 
STRIDE_MNEMONIC=''
```
```
GAIA_RPC_ADDR='' 
GAIA_MNEMONIC=''
```
```
RELAYER_ID='RuesCommunity|Rues#9144' 
```

## Sistem güncellemesi:
```
sudo apt update && sudo apt upgrade -y
```

## Go yüklüyoruz:
```
cd $HOME
wget "https://go.dev/dl/go1.18.3.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go1.18.3.linux-amd64.tar.gz"
rm "go1.18.3.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile
source ~/.bash_profile
```

## GO Relayer v2'yi kurun ve başlatıyoruz:
```
git clone https://github.com/cosmos/relayer.git
cd relayer && git checkout v2.0.0-rc4
make install
rly config init
```

## Strıde .json oluşturuyoruz:

* "key" kısmında "rues" olan kısmı cüzdan adınızı girin.

```
sudo tee $HOME/.relayer/stride.json > /dev/null <<EOF
{
  "type": "cosmos",
  "value": {
    "key": "rues",
    "chain-id": "STRIDE-TESTNET-2",
    "rpc-addr": "http://${STRIDE_RPC_ADDR}",
    "account-prefix": "stride",
    "keyring-backend": "test",
    "gas-adjustment": 1.2,
    "gas-prices": "0.001ustrd",
    "debug": true,
    "timeout": "20s",
    "output-format": "json",
    "sign-mode": "direct"
  }
}
EOF
```

## GAIA .json oluşturuyoruz:

* "key" kısmında "rues" olan kısmı cüzdan adınızı girin.

```
sudo tee $HOME/.relayer/gaia.json > /dev/null <<EOF
{
  "type": "cosmos",
  "value": {
    "key": "rues",
    "chain-id": "GAIA",
    "rpc-addr": "http://${GAIA_RPC_ADDR}",
    "account-prefix": "cosmos",
    "keyring-backend": "test",
    "gas-adjustment": 1.2,
    "gas-prices": "0.001uatom",
    "debug": true,
    "timeout": "20s",
    "output-format": "json",
    "sign-mode": "direct"
  }
}
EOF
```

## Zincirleri yüklüyoruz:
```
rly chains add --file=$HOME/.relayer/stride.json stride
```
```
rly chains add --file=$HOME/.relayer/gaia.json gaia
```

## Anahtara eklenen zincirleri kontrol edelim:
```
rly chains list
```

### Başarılı çıktı aşağıdaki gibi olmalı

```
 1: STRIDE-TESTNET-2     -> type(cosmos) key(✘) bal(✘) path(✘)
 2: GAIA                 -> type(cosmos) key(✘) bal(✘) path(✘)
```

## Cüzdanları aktarıcıya yükleyin:

* "rues" olan kısmı cüzdan adınızla değiştirin.

```
rly keys restore stride rues "${STRIDE_MNEMONIC}"
```
```
rly keys restore gaia rues "${GAIA_MNEMONIC}"
```

## Cüzdan bakiyesini kontrol edin:
```
rly q balance stride
```
```
rly q balance gaia
```

# Burayı dikkatli okuyunuz!

* `nano $HOME/.relayer/config/config.yaml` içine giriyoruz ve {} işeretini değiştirip altta ki kod ile değiştirin:
* Nasıl gözükeceğini altta görselde gösterdim, "stride-gaia" kısmı sola kaymış olacak boşluk atarak yukarıdakilerle aynı hizaya getirin.

```
    stride-gaia:
        src:
            chain-id: STRIDE-TESTNET-2
            client-id: 07-tendermint-0
            connection-id: connection-0
        dst:
            chain-id: GAIA
            client-id: 07-tendermint-0
            connection-id: connection-0
        src-channel-filter:
            rule: allowlist
            channel-list: [channel-0, channel-1, channel-2, channel-3, channel-4]
```

![image](https://user-images.githubusercontent.com/101149671/183388105-c719b822-6547-4b8b-a56a-039f743f78a4.png)


## MEMO ile aktarıcı notunu güncelleyelim:
```
sudo wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/download/v4.23.1/yq_linux_amd64 && chmod +x /usr/local/bin/yq 
yq -i ".global.memo = \"$RELAYER_ID\"" $HOME/.relayer/config/config.yaml
```

## Kontrol edin
```
rly paths list
```

## Başarılı çıktı:

* NOT: Yukarıda ki komutun çıktısı bu

```
0: stride-gaia          -> chns(✔) clnts(✔) conn(✔) (STRIDE-TESTNET-2<>GAIA)
```

## Hizmet oluştururalım:
```
sudo tee /etc/systemd/system/relayerd.service > /dev/null <<EOF
[Unit]
Description=GO Relayer v2 Service
After=network.target
[Service]
Type=simple
User=$USER
ExecStart=$(which rly) start stride-gaia -p events
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```
## Hizmeti oluşturduk şimdi başlatalım:
```
sudo systemctl daemon-reload
systemctl enable relayerd
systemctl start relayerd
```

## Logları kontrol edelim:
```
screen -S relayer
```
```
journalctl -u relayerd -f -o cat
```

## Relayer transfer yapıyoruz:

* adres kısmına kendi adreslerinizi girin.
* Bu işlemleri yapmanız için cüzdanınızda bakiye olmalı, yoksa [Discord kanalı](https://discord.gg/3XSNGPDN)

```
rly transact transfer stride gaia 1000ustrd cosmoadresi channel-0 --path stride-gaia
```
```
rly transact transfer gaia stride 1000uatom strideadresi channel-0 --path stride-gaia
```






