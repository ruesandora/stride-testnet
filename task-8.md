<h1 align="center"> RELAYER v2 task-8</h1>


## BU KISIM STRIDE ICERSINDE CALISTIRILACAK

* INDEXER açma, hem STRIDE hemde [GAIA](https://github.com/ruesandora/GAIA) için.. Hermesi yukardan GAIA-STRIDE ile kuranlar bu komutu atlasın.

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
    "chain-id": "STRIDE-TESTNET-4",
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
 1: STRIDE-TESTNET-4     -> type(cosmos) key(✘) bal(✘) path(✘)
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
            chain-id: STRIDE-TESTNET-4
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
0: stride-gaia          -> chns(✔) clnts(✔) conn(✔) (STRIDE-TESTNET-4<>GAIA)
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

# BİTMEDİ DEVAMI VAR:

## Burada ki repoyu forkluyoruz:

* [cosmos/relayer](https://github.com/cosmos/relayer)

## configs'in içine giriyoruz:

![image](https://user-images.githubusercontent.com/101149671/183974578-fa6c9b0b-9f33-4831-a84f-619d2cf225ac.png)

## Create new file diyoruz ve Stride adında dosya oluşturuyoruz:

![image](https://user-images.githubusercontent.com/101149671/183974813-50dc348e-1dac-4fbe-9cd9-930089628f7c.png)

## Şimdi 2 dosya oluşturuyoruz:

* İlki chains
* İkinci paths adında dosyalar:
* Dosya oluştururken sonlarına / işareti koyalım. (2. görsele bakın)

![image](https://user-images.githubusercontent.com/101149671/183974963-1c598e6f-ce83-47c4-9eb3-a99f1e68c896.png)

* /

![image](https://user-images.githubusercontent.com/101149671/183975218-b5ffae4d-2e17-4f7a-af18-9b5532020069.png)

## Şimdi stride.json ve gaia.json oluşturup içlerini dolduracağız.

![image](https://user-images.githubusercontent.com/101149671/183975140-86db0a46-5c4b-45f0-9db0-59ccdf089e51.png)


## Gaia nodumuza giriyoruz:

* Altta ki komutu giriyoruz ve çıktıyı kopyalıyoruz.
* Kopyaladığımız çıktıyı yukarıda oluşturduğumuz gaia.json dosyasına ekliyoruz.

```
nano $HOME/.relayer/gaia.json
```
![image](https://user-images.githubusercontent.com/101149671/183975788-17467305-8ead-4e75-8c89-c3541fd7f46e.png)

## Stride nodumuza giriyoruz:

* Altta ki komutu giriyoruz ve çıktıyı kopyalıyoruz.
* Kopyaladığımız çıktıyı yukarıda oluşturduğumuz stride.json dosyasına ekliyoruz.
* Tıpkı yukarda ki gibi.

```
nano $HOME/.relayer/stride.json
```

## Şimdi yukarıda confingin içine girip stride oluşturduk onunda içine girip chains ve paths oluşturduk, chains'in içine gaia ve stride ile doldurduk, şimdi paths'ın içine girelim.

* paths'ın içine stride-gaia.json oluşturalım

![image](https://user-images.githubusercontent.com/101149671/183976375-bda2ac1c-9e22-4ea1-a302-4d507d3eaacd.png)


## stride-gaia.json'un içine altta ki kodu girin ve kaydedin.

```
{
  "src": {
    "chain-id": "STRIDE-TESTNET-4",
    "client-id": "07-tendermint-0",
    "connection-id": "connection-0"
  },
  "dst": {
    "chain-id": "GAIA",
    "client-id": "07-tendermint-0",
    "connection-id": "connection-0"
  },
  "src-channel-filter": {
    "rule": "allowlist",
    "channel-list": ["channel-0", "channel-1", "channel-2", "channel-3", "channel-4"]
  }
}
```

## Şimdi burada yaptığımız "forku"  - "kendi yaptığınız forku" formda bir yere eklersiniz.

* tekrar altını çiziyorum size ait forku, sol üstte ruesandora değil siz yazacaksınız.

![image](https://user-images.githubusercontent.com/101149671/183977194-e0f86d5b-fa23-4ba5-a0ea-a7590f28a94c.png)
