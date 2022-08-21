
<h1 align="center"> STRIDE-GAIA HERMES task-7 </h1>

# Bu rehber, Hermes'i Stride STRIDE-TESTNET-4 nodeunuzun kurulu olduğu sunucu ile aynı sunucuya kurulum yapacağınızı varsayar ve yapılandırmalar ona göre ayarlanmıştır. 

### GAIA kurmadıysanız: [GAIA Rehberi](https://github.com/ruesandora/GAIA)

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
id = 'STRIDE-TESTNET-4'
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
hermes keys restore STRIDE-TESTNET-4 -m "$MNEMONIC1"
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
hermes tx raw ft-transfer GAIA STRIDE-TESTNET-4 transfer channel-0 1000 -d ustrd -r strıdecüzdanı -t 60 -o 100
```
```
hermes tx raw ft-transfer STRIDE-TESTNET-4 GAIA transfer channel-0 1000 -d uatom -r gaıacüzdanı -t 60 -o 100
```

## Explorer'dan işlemleri kontrol edelim: [Explorer Linki](https://poolparty.stride.zone/GAIA/staking)

* tx hash'a tıklıyoruz:

![image](https://user-images.githubusercontent.com/101149671/183289537-8b1f65ae-4ea1-4fa5-ba46-74abd9e2e5f5.png)

* Yukarıda hatırlarsınız memo (imza) eklemiştik:

![image](https://user-images.githubusercontent.com/101149671/183290069-ea2bdf10-a1d1-4b6e-a308-2797f9f1f04f.png)
