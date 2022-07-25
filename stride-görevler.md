# Selamlar, stride için gerekli görevleri yapıyoruz, çok basit.


# Likidite - Staking görevi: 

* Cüzdan adınızı ekleyin.

```
strided tx stakeibc liquid-stake 1000 uatom --from CÜZDAN ADINIZ --chain-id STRIDE-1 --gas auto -y
```

# Redeem görevi:

* Cosmos: cüzdanı kısmına KEPLR'da yazan GAIA ağını ekleyın.
* From: kısmı cüzdan adınız
* GAIA ağını eklemek için : https://twitter.com/Ruesandora0/status/1550485313243545601?s=20&t=PWfmmnIxju9LN-kGW5VznA

```
strided tx stakeibc redeem-stake 500 GAIA cosmos1vm6wnmvxugqj8k6s6d2cktgctc550qaq50kyye  --chain-id STRIDE-1 --from rues --gas 500000 -y
```

# Bu görevin Komutunda düzenlemeniz gereken tek kısım stride adresi, adresi explorer üzerinde ki cüzdan adresiniz yapın. (Account: https://stride.explorers.guru/)

* GÖRSELDE Kİ ÇIKTIYI ALMANIZ UZUN SÜREBİLİR 10-15DK ARALIKLARLA DENEYIN

```
strided q records list-user-redemption-record --output json | jq --arg stride1hfjy2cr09hddsgzp84nuue08tx8thhv4xy7gth '.UserRedemptionRecord | map(select(.sender == $WALLET_ADDRESS))'
```

* GÖRSELDE Kİ ÇIKTIYI ALMANIZ UZUN SÜREBİLİR 10-15DK ARALIKLARLA DENEYIN
![image](https://user-images.githubusercontent.com/101149671/180779195-57e97d6c-5658-4d80-af22-d704a8c0cd79.png)


# IBC görevi:

* Sei adresi yazan yer, kendi adresiniz olacak
* From cüzdan adınız olcak.
* Altta channeleri vericem istediğiniz channela gönderin.
* Stafi: channel-15
* Sei: channel-22 
* Altta ki 

```
strided tx ibc-transfer -y transfer transfer channel-22 sei1654kj35pszp4t49wcglwcg0cwlxg5vvw8rv32t 10000ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2  --chain-id STRIDE-1 --from rues
```

# FORM DOLDURUN

https://docs.google.com/forms/d/e/1FAIpQLSfdDrh5-WIsY6LlwVElFfoWR8dZdlE70vHujIMBiD-4USvpsg/viewform

# İŞLEMLER BU KADAR, GÜNCELLEME GELİRSE EKLERİM
