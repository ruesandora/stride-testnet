# Bu rehber, Hermes'i Stride STRIDE-TESTNET-2 nodeunuzun kurulu olduğu sunucu ile aynı sunucuya kurulum yapacağınızı varsayar ve yapılandırmalar ona göre ayarlanmıştır. (Bu kısım sadece STRIDE node içinde çalıştırılacak)

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
