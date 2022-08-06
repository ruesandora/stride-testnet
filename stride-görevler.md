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

# IBC, bu görevler arasında yok ama neden yapmayalım :):

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

### Arkadaşlar normal şartlarda buraları kendiniz yapmanız gerekiyor, benim paylaşmamam gerekiyor ama size yol gösterici bir şekilde rehber paylaşacağım. Lütfen unutmayın bu sorular "TELEGRAMDA" veya "DİSCORDDA" sormanız yasak.. Stride Türkiye grubunun Resmi kanal olduğunu unutmayın, burada yalnızsınız ve sizin gayretinize kalmış. (Normalde bir sürü şey yazmıştım ama buna izin yokmuş :/)

![image](https://user-images.githubusercontent.com/101149671/183241967-5b0cddee-df42-4722-a372-974e8ad1369d.png)

### Gördüğünüz gibi günlerdir bu dertle uğraşıyorum, tamamen yalnızsınız, telegramda sormayın (telegram bana ait değil resmi Türkiye orası):

![image](https://user-images.githubusercontent.com/101149671/183242178-3a251579-6cca-4e4f-bbc8-d096bc2c2c0e.png)

# Hermes:

* GÖREVLER ARASINDA YOK, YAZDIM BOŞA GİTMESIN DİYE LAZIM OLACAKTIR İLERİDE

* RELAYER YAZMAM MÜSADE EDİLİRSE YAZACAĞIM. (discordda relayer kanalı mevcut istersenız ordan kopya çekin)

* NOT: Bu rehber, Hermes'i Stride STRIDE-TESTNET-2 nodeunuzun kurulu olduğu sunucu ile aynı sunucuya kurulum yapacağınızı varsayar ve yapılandırmalar ona göre ayarlanmıştır. ( Bu kısım sadece STRIDE node içinde çalıştırılacak)

* Kodu girdikten sonra: `hermes 0.15.0+4e83aae` çıktısı alırsınız

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

## Değişkenleri ayarlayın Sei atlantic-1 ( Bu kısım sadece SEI node içinde çalıştırılacak)

* Sei node kurmadıysanız farklı bir node ile de yapabilirsiniz sei olan yerleri örn: stafihub - teritori vs diye değişerek.
* Ben sei'den yola gidiyorum çünkü yayında anlattığım senaryoya göre hem sei görevi hemde stride görevi yapmış olacağız.

```
PORTN=$(grep -A 3 "\[p2p\]" ~/.sei/config/config.toml | egrep -o ":[0-9]+")
sed -i.bak 's/external_address = ""/external_address = "'"$(curl -4 ifconfig.co)"''$PORTN'"/g' $HOME/.sei/config/config.toml

PORTR=$(grep -A 3 "\[rpc\]" ~/.sei/config/config.toml | egrep -o ":[0-9]+")
sed -i.bak -e "s%^laddr = \"tcp://127.0.0.1$PORTR\"%laddr = \"tcp://0.0.0.0$PORTR\"%" $HOME/.sei/config/config.toml
sed -i.bak -e "s/indexer *=.*/indexer = \"kv\"/g" $HOME/.sei/config/config.toml

systemctl restart seid
```

## Aşağıda ki işlemden sonra iki çıktı alacaksınız:

* IP:PORT formatında ki bu iki çıktıyı bir yere not edin! 
* Bir sonra ki aşamada kullanacağız. Bu bizim GRPC değerimiz olacak.
* x.x.x.16:12090 ve x.x.x.16:12657 gibi örnek çıktı alacaksınız 
* son sayılar herkeste aynı olmaz kimisinde 12657 olur kimisinde 9090 olur
* İlk komut GRPC ikinci komut RPC çıktısı (komutun içinde de yazar)

```
echo "$(curl -s ifconfig.me)$(grep -A 6 "\[grpc\]" ~/.sei/config/app.toml | egrep -o ":[0-9]+")"
```
```
echo "$(curl -s ifconfig.me)$(grep -A 3 "\[rpc\]" ~/.sei/config/config.toml | egrep -o ":[0-9]+")"
```
## Stride STRIDE-TESTNET-2 için değişkenleri ayarlayın: 

* Bu kısım ve bundan sonrası sadece STRIDE node içinde çalıştırılacak
* Bir önce ki sunucumuzda iki çıktı almıştık, şimdi onları kullanacağız. 
* GRPC olarak kullanacağız diye belirttiğimiz IP:PORT (x.x.x.16:12090) formatında ki çıktıyı, aşağıda ki GRPC karşısında ki "" içine yazın.
* Aynı şekilde, RPC olarak kullanacağız diye belirttiğimiz IP:PORT (x.x.x.16:12090) formatında ki çıktıyı,aşağıda ki RPC karşısında ki "" içine yazın.
* Yukarda yazdım UNUTMAYIN! Birinci GRPC ikinci RPC çıktısı. (birinci ikinci diye değil GRPC-RPC diye hitap edeceğim)
* Doldurun "" işaretlerini (not edin bir yere)

```
GRPC=""
RPC=""
```

## Cüzdan Mnemoniğinizi, aşağıda ki MNEMONİC karşısında ki "" içine girin:

* İlk MNEMONIC STRIDE wallete ait, 2. MNEMONIC SEI wallete ait (veya kurduğunuz başka testnet)
* Mnemınic = 24 kelime

```
MNEMONIC1=""
MNEMONIC2=""
```

## Relayerlar'da özel size ait imzamız olsun istemez miyiz? 

* İstediğiniz bir ismi, aşağıda MEMO karşısında ki "" içine girin. 
* MEMOyu kendinize göre değiştirin

```
MEMO="RuesCommunity-Rues"
```
## Şimdi, bu komutları çalıştırın
```
sed -i.bak 's/external_address = ""/external_address = "'"$(curl -4 ifconfig.co)"':26656"/g' $HOME/.stride/config/config.toml
PORTR=$(grep -A 3 "\[rpc\]" ~/.stride/config/config.toml | egrep -o ":[0-9]+")
PORTG=$(grep -A 6 "\[grpc\]" ~/.stride/config/app.toml | egrep -o ":[0-9]+")
```

## Tek Seferde Terminalde Çalıştırın
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
memo_prefix = 'MEMO'
trust_threshold = { numerator = '1', denominator = '3' }

[[chains]]
id = 'atlantic-1'
rpc_addr = 'http://$RPC'
grpc_addr = 'http://$GRPC'
websocket_addr = 'ws://$RPC/websocket'
rpc_timeout = '10s'
account_prefix = 'sei'
key_name = 'sei'
address_type = { derivation = 'cosmos' }
store_prefix = 'ibc'
default_gas = 300000
max_gas = 15000000
gas_price = { price = 0.000001, denom = 'usei' }
gas_adjustment = 0.1
max_msg_num = 15
max_tx_size = 100000
clock_drift = '5s'
max_block_time = '30s'
trusting_period = '5hours'
memo_prefix = 'MEMO'
trust_threshold = { numerator = '1', denominator = '3' }
EOF
```
## Cüzdanınızı içe aktarın

* Direkt kodu yapıştırabilirsiniz, mnemonic gerekli değil.

```
hermes keys restore STRIDE-TESTNET-2 -m "$MNEMONIC1"
hermes keys restore atlantic-1 -m "$MNEMONIC2"
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

## Servisi başlatın
```
systemctl daemon-reload
systemctl enable hermesd
systemctl start hermesd
```

## Yapılandırmayı kontrol edin

* çıktı da şunu görmelisiniz, ikisinden birisi yazar.
* Success: "validation passed successfully"
* Success: "configuration is valid"

```
hermes config validate
```


## Nodeların doğru çalışıp çalışmadığını kontrol edin
```
hermes health-check
```

### Çıktı şu şuna benzer olmalı

```
2022-06-28T23:38:58.780845Z  INFO ThreadId(01) using default configuration from '/username/.hermes/config.toml'
2022-06-28T23:38:58.782408Z  INFO ThreadId(01) [stafihub-public-testnet-3] performing health check...
2022-06-28T23:38:58.806784Z  INFO ThreadId(01) [stafihub-public-testnet-3] chain is healthy
2022-06-28T23:38:58.807543Z  INFO ThreadId(01) [atlantic-1] performing health check...
2022-06-28T23:38:58.816811Z  INFO ThreadId(01) [atlantic-1] chain is healthy
Success: performed health check for all chains in the config
```

## Bu kısımda screen oluşturup servisi içinde çalıştırıralım.
```
screen -S hermes
```

## Bu sırada hermes loglarını kontrol etmek için başlaması için 5dk bekleyin

```
journalctl -u hermesd.service -fo cat
```

## Aşağıdaki komut hermes transfer komusu Stride tan Sei ağına 1000 ustrd yolladım.
```
hermes tx raw ft-transfer atlantic-1 STRIDE-TESTNET-2 transfer channel-271 1000 -t 60 -o 100
```




