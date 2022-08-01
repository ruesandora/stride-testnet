<h1 align="center">Selamlar, bugün Stride görevlerini  yapıp form dolduracağız, floodu detaylı okuyunuz, çünkü elenme durumu söz konusu </h1>




# Bazı görevlerde yalnızsınız, kişisel görevler, ben açıklama bırakacağım sizin yapmanız gerekiyor, "ANCAK":

* Kişisel görevlerde başkasının görevini veya PR'ını (pull request) kopyalamak veya discord/ telegram kanallarında sormak yasak.
* Sadece #incentive-tasks discord odasında sorabilirsiniz görev sorularını.
*


 

## 🗡️ Adversarial Tasks
| # | Pts |  Task  | Evidence |
| -- | -- | ------------- |:-------------:|
| **1** | 750 | Stride'ın [core repo'sunda](https://github.com/Stride-Labs/stride) bir hata bulun. | Yaparsanız forma PR'ınızın linkini ekleyin|| **5** | 100 | spam network with transactions | writeup on your results and link to the blocks you spammed |
| **2** | 750 | cause the chain to halt through normal usage of the network | writeup and link to your address |
| **3** | 1000 | steal user testnet funds (any attack approach is allowed!) | writeup and link to transactions involved |


## 📚 Community Tasks
| # | Pts |  Task  | Evidence |
| -- | -- | ------------- |:-------------:|
| **4** | 50 | resolve over 20 users questions in discord (high quality answers only) | your discord handle and link to a few of the messages  |
| **5** | 200 | contribute to creating the stride support lab (message samuel on Discord to begin) | submit writeup on your contributions |

## 🌊 Product Tasks
| # | Pts |  Task  | Evidence |
| -- | -- | ------------- |:-------------:|
| **6** | 50 | complete the stake, redeem, and claim flow (including 6hr unbonding) | link to all the txs: liqstake, redeem, claim |

## 🛰  Relayer Tasks 

| # | Pts |  Task  | Evidence |
| -- | -- | ------------- |:-------------:|
| **7** | 100 | run a relayer on ICA channels specified in #validator-announcements | link to the stride relayer account and to one relayed tx |
| **8** | 250 | relay using the new [v2 go relayer](https://github.com/cosmos/relayer/releases/tag/v2.0.0-rc4)      | link to packets relayed and link to the configured relayer fork on your github |
| **9** | 750 | relay interchain queries using the new [v2 go relayer](https://github.com/cosmos/relayer/releases/tag/v2.0.0-rc4) | link to ICQ packets relayed and link to the configured relayer fork on your github |

## ⚡ Validator Tasks 

| # | Pts |  Task  | Evidence |
| -- | -- | ------------- |:-------------:|
| **10** | 100 | run validator for at least 7 days (being inactive is OK, it still qualifies) | link to your validator address |
| **11** | 10 | delegate to another validator  | link to the delegation transaction |



<h1 align="center">BURASI ESKİ GÖREV BİTTİ, OKUMANIZA GEREK YOK, FORM İLE ALAKASI YOK, ESKİ AĞA AİT</h1>


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
