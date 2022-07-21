<h1 align="center">Stride - Poll Party! </h1>

### Selamlar bugün Stride node testnetine katılacağız. SORULAR İÇİN: https://t.me/StrideTurkish

![image](https://user-images.githubusercontent.com/101149671/180230551-dbc0d5f0-b087-483f-9e7a-95711a820209.png)


# Kurulum:

```
wget -q -O stride.sh https://api.rues.info/stride.sh && chmod +x stride.sh && sudo /bin/bash stride.sh
```

# Cüzdan oluşturma: (not edin kaydedin)
```
strided keys add <walletName>
```

# Discordan test tokeni alma: https://discord.gg/4B4cbvCh

![image](https://user-images.githubusercontent.com/101149671/180231116-4eaae21a-184c-4204-a3f1-e7ac945e1455.png)

# Validator oluşturma:
```
strided tx staking create-validator \
--amount=9900000ustrd \
--pubkey=$(strided tendermint show-validator) \
--moniker=RuesValidator \
--chain-id=STRIDE-1 \
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

# Explorer kontrol: https://stride.explorers.guru/validator/stridevaloper1vm6wnmvxugqj8k6s6d2cktgctc550qaq53jyus

# sorular için: https://t.me/StrideTurkish

# Hesaplar:

[<img src="https://cdn-icons-png.flaticon.com/512/733/733579.png" width="16px"> Twitter   ](https://twitter.com/Ruesandora0) 

[<img src="https://cdn-icons-png.flaticon.com/512/1336/1336494.png" width="16px"> Forum   ](https://forum.rues.info/index.php)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Announcement   ](https://t.me/RuesAnnouncement)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Chat   ](https://t.me/+-l6GpqiNOxFiMTVk)

[Discord](https://discord.gg/ruescommunity)
