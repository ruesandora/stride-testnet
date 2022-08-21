
<h1 align="center"> RELAYER ICQ task-9</h1>


## İkili dosyaları indirin ve oluşturun
```
cd $HOME
git clone https://github.com/Stride-Labs/interchain-queries.git
cd interchain-queries
go build
cd
sudo mv interchain-queries /usr/local/bin/icq
```

## ICQ için ana sayfa dizini ve yapılandırma dosyası oluşturacağız

* öncesinde GAIA için RPC ve GRPC IP:PORT bilgilerini almamız lazım şimdi GAIA node geçiyoruz

### GAIA

* Aşağıdaki çıktıyı bir sonra ki aşamada GRPC olarak kullanacağız.
```
echo "$(curl -s ifconfig.me)$(grep -A 6 "\[grpc\]" ~/.gaia/config/app.toml | egrep -o ":[0-9]+")"
```
## Aşağıdaki çıktıyı bir sonra ki aşamada RPC olarak kullanacağız.
```
echo "$(curl -s ifconfig.me)$(grep -A 3 "\[rpc\]" ~/.gaia/config/config.toml | egrep -o ":[0-9]+")"
```

# STRIDE

## STRIDE'dan alalım RPC-GRPC bilgileri.

* içinden RPC değerimizi alalım. (bir önce ki floodlarda göstermiştim nasıl alınacağını)
```
nano $HOME/.stride/config/config.toml
```
* içinden GRPC değerimizi alalım 
```
nano $HOME/.stride/config/app.toml
```

## Tek Seferde Terminalde Çalıştırın
```
cd $HOME && mkdir .icq
sudo tee $HOME/.icq/config.yaml > /dev/null <<EOF
default_chain: stride-testnet
chains:
stride-testnet:
    key: wallet
    chain-id: STRIDE-TESTNET-4
    rpc-addr: http://127.0.0.1:16657      # use your own Stride GRPC endpoint here
    grpc-addr: http://127.0.0.1:16090     # use your own Stride GRPC endpoint here
    account-prefix: stride
    keyring-backend: test
    gas-adjustment: 1.2
    gas-prices: 0.001ustrd
    key-directory: /root/.icq/keys
    debug: false
    timeout: 20s
    block-timeout: ""
    output-format: json
    sign-mode: direct
gaia-testnet:
    key: wallet
    chain-id: GAIA
    rpc-addr: http://165.227.165.197:23657       # use your own Gaia RPC endpoint here
    grpc-addr: http://165.227.165.197:23090     # use your own Gaia GRPC endpoint here
    account-prefix: cosmos
    keyring-backend: test
    gas-adjustment: 1.2
    gas-prices: 0.001uatom
    key-directory: /root/.icq/keys
    debug: false
    timeout: 20s
    block-timeout: ""
    output-format: json
    sign-mode: direct
cl: {}
EOF
```

## Cüzdanları içe aktaralım.
```
icq keys restore --chain stride-testnet rues
```
```
icq keys restore --chain gaia-testnet rues
```

## ICQ hizmeti oluşturun
```
sudo tee /etc/systemd/system/icqd.service > /dev/null <<EOF
[Unit]
Description=Interchain Query Service
After=network-online.target

[Service]
User=$USER
ExecStart=$(which icq) run --debug
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
## Hizmetini başlatın
```
sudo systemctl daemon-reload
sudo systemctl enable icqd
sudo systemctl restart icqd
```

## Bitiriyoruz:
```
screen -S icq
```
```
journalctl -u icqd -f -o cat
```
```
rly transact update-clients stride-gaia
```
```
rly transact transfer stride gaia 1000ustrd cosmosadresi channel-0 --path stride-gaia
```
```
rly transact transfer gaia stride 1000uatom strideadresi channel-0 --path stride-gaia
```

# Şükürler olsun..








