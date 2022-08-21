
<h1 align="center">Selamlar, bugün Stride görevlerini  yapıp form dolduracağız, floodu detaylı okuyunuz, çünkü ELENME durumu söz konusu </h1>

# Bazı görevlerde yalnızsınız, kişisel görevler, ben açıklama bırakacağım sizin yapmanız gerekiyor, "ANCAK":

* Kişisel görevlerde başkasının görevini veya PR'ını (pull request) kopyalamak veya discord/telegram kanallarında sormak yasak.
* Sadece #incentive-tasks discord odasında sorabilirsiniz görev sorularını.
* Görevleri merak ediyorsanız: [Görev Listesi](https://github.com/Stride-Labs/testnet/tree/main/incentivized-testnet)
* Bunlar dışında sorunuz varsa: [Stride Türkiye](https://t.me/StrideTurkish)
* Görev formu, her görev için 1 form doldurulacak [Form](https://docs.google.com/forms/d/e/1FAIpQLSeoZEC5kd89KCQSJjn5Zpf-NQPX-Gc8ERjTIChK1BEbiVfMVQ/viewform)

<h1 align="center">Paylaşabileceğim görevlerin rehberi: </h1>

# Likidite - Staking görevi task-6: 

* ÖNEMLİ: Altta yapacağınız işlemlerin hepsini TX'ini alıp explorerde aratın, succes olmuşsa TX'i kaydedin. [Explorer](https://poolparty.stride.zone/STRIDE)
* Cüzdan adınızı ekleyin.

```
strided tx stakeibc liquid-stake 1000 uatom --from CÜZDAN ADINIZ --chain-id STRIDE-TESTNET-4 --gas auto -y
```

# Redeem görevi task-6:

* Cosmos: cüzdanı kısmına KEPLR'da yazan GAIA ağını ekleyın.
* From: kısmı cüzdan adınız
* GAIA ağını eklemek için : [Gaia](https://twitter.com/Ruesandora0/status/1550485313243545601?s=20&t=PWfmmnIxju9LN-kGW5VznA)

```
strided tx stakeibc redeem-stake 500 GAIA cosmos1vm6wnmvxugqj8k6s6d2cktgctc550qaq50kyye  --chain-id STRIDE-TESTNET-4 --from CÜZDANADIN --gas 500000 -y
```

# Claim görevi task-6:

* Şu an burada claim edilcek token gözükmüyor, hata alabilir herkes, bende aldım. İsterseniz deneyin, düzelirse paylaşırım telegramda

```
strided tx stakeibc claim-undelegated-tokens GAIA 296 stride1d6v2gd0hzzg8hp7jzkfsp8uyqd5hh5tsnvjxuv --chain-id STRIDE-TESTNET-4 --from rues -y
```

## Bu üçü tek göreve karşılık geliyor (6 numaralı görev)

![image](https://user-images.githubusercontent.com/101149671/183288571-5c78da8f-f01d-412a-922e-0b18b66c7751.png)

## Delege görevi task-11: 
```
strided tx staking delegate stridevaloper1d6v2gd0hzzg8hp7jzkfsp8uyqd5hh5tssek6sf 1000000ustrd --from=cüzdanismin --chain-id STRIDE-TESTNET2 --gas=auto
```
# IBC, bu, görevler arasında yok ama neden yapmayalım :):

* From cüzdan adınız olcak.
* Komutu direkt kullanabilirsiniz

```
strided tx ibc-transfer -y transfer transfer channel-22 sei1654kj35pszp4t49wcglwcg0cwlxg5vvw8rv32t 10000ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2  --chain-id STRIDE-TESTNET-4 --from rues
```

## Kolay görevler:

* 7 gün validator çalıştırmak (validator linki verırsınız forma) - task-10
* Discordda 20 kişinin sorusunu cevaplamak - task-4

<h1 align="center">LÜTFEN BURAYI ÇOK DİKKATLİ OKUYUN, ÖDÜL HAKKINIZI KAYBETMEYİN </h1>

# 7/8/9. Görevler:

### Arkadaşlar normal şartlarda buraları kendiniz yapmanız gerekiyor, benim paylaşmamam gerekiyor, bunu yapmama müsade edilmiyor, herkesin kendisi yapılması konusunda ısrarla belirtilmiş, yaklaşık 4 gündür bu konu ile ilgileniyorum.. Lütfen unutmayın bu sorular "TELEGRAMDA" veya "DİSCORDDA" sormanız yasak.. Stride Türkiye grubunun Resmi kanal olduğunu unutmayın, burada yalnızsınız ve sizin gayretinize kalmış. (Normalde bir sürü şey yazmıştım ama buna izin yokmuş :/)

### AMA size rehber olması açısından bir şeyler göstereceğim, sorular için sadece discordu kullanabılıyorsunuz relay 2 için

![image](https://user-images.githubusercontent.com/101149671/183241967-5b0cddee-df42-4722-a372-974e8ad1369d.png)

### Gördüğünüz gibi günlerdir bu dertle uğraşıyorum, tamamen yalnızsınız, telegramda sormayın (telegram bana ait değil resmi Türkiye orası):

![image](https://user-images.githubusercontent.com/101149671/183242178-3a251579-6cca-4e4f-bbc8-d096bc2c2c0e.png)


### [GAIA Kurmak isterseniz](https://github.com/ruesandora/GAIA)

### [Görev 7 - task-7](https://github.com/ruesandora/stride-testnet/blob/main/task-7.md)

### [Görev 8 - task-8](https://github.com/ruesandora/stride-testnet/blob/main/task-8.md)

### [Görev 9 - task-9](https://github.com/ruesandora/stride-testnet/blob/main/task-9.md)















