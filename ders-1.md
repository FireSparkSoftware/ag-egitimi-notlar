# WIFI Eğitimi 1. Ders Notları

# IEEE 802. Standartları
Yaygın kullanılanlar:

- 802.3 CSMA / CD (Ehternet)
- 802.11 Wireless Lan (WLAN)
  - 802.11a
  - 802.11b
  - 802.11e
  - 802.11g
  - 802.11i
- 802.15 Wireless Personal Area Network (WPAN) (Ör. Bluetooth)

PAN - Personal Area Network
LAN - Local Area Network
MAN - Metropolitan Area Network
WAN - Wide Area Network

## IEEE 802.11 Standartları
802.11 ailesi sadece hızı değil bir çok şeyi tarif etmektedir.

Örneğin:
- 802.11a: 5GHz, 54Mbps
- 802.11b: 2.4GHz, 11Mbps
- 802.11e: Quality of Service (QoS) 
- 802.11i: Security

Hiçbir wireless için vaadedilen hızlar tamamen alınamaz. Ortamda çok parazit vardır ve kontrol bitleri çok büyük alan kaplar. Verimi yarıya düşürür.

Hızlar:
- 802.11g 54Mbps
- 802.11n 300Mbps (up + down: 150Mbps) (2x2 MIMO)
- 802.11n 450Mbps (3x3 MIMO)
- 802.11ac 1300 Mbps (3x3 MIMO)

Wireless'da aynı anda birden fazla kişi haberleşemez. Bir paket yollanırken diğer kullanıcılar bekler. Herkes aynı frekansı kullanıyor.

Evde 10 cihaz aynı anda haberleşme isteğinde bulunursa maalesef diğer kullanıcıları beklemek durumunda kalırlar. Var olan hızımız da 10'a bölünecektir.

100Mbps kablolu bağlantı bize özeldir ve ben haberleşirken diğer cihazlar beklemez. Full dublextir ve 100Mbps download yaparken 100Mpbs upload yapılabilir.

## MIMO Teknolojisi
Wireless yayını dairesel olarak etrafı kaplayacaktır. Hedefe ulaşan sinyal, duvardan gelen sinyale göre daha hızlıdır ve sonradan gelen sinyal önceki sinyali bozmaktadır. (multipath distortion) Çözüm ise, aynı frekans aralığında aynı anda birden fazla paketin birden çok yöne dağıtarak bant genişliği arttırılmasıdır. Bu şekilde hız yükseltmesi yapılmakta.

## SSID
Service Set Identifier 32 karakterdir.

# Lisanssız Frekans Bantları
Yaygın kullanılan frekans aralıkları:

- 2.4 Ghz - 2.4835 Ghz (83.5 MHz) 802.11b ve 802.11g
- 5 GHz 802.11a, 802.1ac teknolojisi kullanır.

## 2.4 GHz Kanal Tahsisleri
14 kanal vardır. 5MHz arttırılarak oluşturulmuştur. 1 kanal 24MHz harcıyordu (şu an 20), 2.4GHz aralığı 2400MHz'ten başladığından dolayı bunun tam ortası olan 2412MHz'ten başlanılmıştır.

- 1: 2412MHz
- 2: 2417MHz
- 3: 2422MHz
- ...: ...
- 11: 2462MHz
- 12: 2467MHz (Amerika bölgesi bu ve altını kullanmaz.)
- 13: 2472MHz 
- 14: 2484MHz (Sadece Japonya bölgesi kullanır.)

11 ayrı ap aynı anda haberleşemez bunun sebebi ise:

1 yayın 20MHz yer kaplıyor. İlk yayın aralıklarını 5MHz ileri sarınca 1. kanal ile 2. kanal iç içe girmektedir. Aynı şekilde 3, 4 ve 5. kanallar da çakışmaktadır. En mantıklı çözüm ise birbirleriyle çakışmayan yayınları tercih etmektir. Bunlar da: 1, 6 ve 11'dir. Ara kanalları da seçebiliriz.

Japonlar ise 14. kanalı daha fazla kaydırmaktadırlar. Bu sayede aynı noktada 4 farkı cihaz bulundurabilmektedirler.

802.11n de ise iki kanalı birleştirip tek yayın yaparak hızı arttırabiliriz, fakat aynı yere aynı alanı kaplayan ikinci bir cihaz yerleştiremiyoruz.

## 5.GHz Kanalları
UNII bantları kullanılmakta. 19 ayrı kanal var ve 2.4GHz'e göre daha çok kanal var demek olmakta. 19 ayrı cihazı 19 farklı yere koyabilmekteyiz. Amerika bölgesi UNII-3 bandını da kullanarak 4 ilave kanal kullanabilmekte.

Yüksek hızlara çıkabilmek için kanallar daha geniş frekans aralıkları kullanmaktadır. Daha geniş frekans aralıkları ise kanal sayılarını düşürmektedir.

Örneğin Avrupa standartlarında 20MHz ile ayrılan 19 ayrı kanal varken 40MHz ile bu sayı 10 kanala, 80MHz ile 5 ve 160MHz ile 2 kanal kullanılabilmekte.

# Sinyal Gücü, Filtreleme ve dBm
Çakışmalar her zaman olmaktadır ve hızımızı düşürmektedir. Üst üste binen yayınlarda güçler birbiri ile aynı değil ise filtreleme yardımı ile bizim iletişimimiz diğerlerinden ayırılabiliyor.

dBm - ile belirtilmesinin sebebi, sinyalin bize gelmesi sırasında azalmasıdır ve bize gelene kadar gerçekleşen azalma miktarını belirtmektedir.

# Anten Yayın Paternleri
Antenin konumu ve doğrultusu sinyal gücüne etki etmektedir. Çubuk antenler tam üstlerine çok az yayın verirler. Bu nedenle evimizde yatayda yayın için çubuk anteni dik tutmakta fayda var. Cihaza entegre antenlerin nasıl çalıştıkları ve bu cihazların konumları önemli detaylardır.

# Kapsama Alanını Genişletme

## Kazancı Yüksek Anten Kullanmak
Ampülün etrafına aynalar koyarak ışığın gücünü arttırmak gibi reflektörler de yayının daha geniş değil de daha uzağa gitmesi gibi etkiler oluşturabiliyor. Reflektörler pasiflerdir ve yaptıkları iş bunlardır. Evlerde kullandığımız antenler genelde 2.4GHz 2.2dBi değerindedir.

## İkinci Bir Cihaz Takma

### Kablosuz uzatma
Fazladan bir AP ile yayın alanını genişletmektir. İkinci AP'in SSID'sini ilk AP ile aynı tutmakta fayda vardır çünkü salondan oturma odasına geçerken çok az yayın kaybı yaşarsınız. Ayrıca bu iki AP'in kanallarını farklı tutmak önemli çünkü yayınlar üst üste binebilir ve birbirini bozabilir. Örneğin birini 1 birini 6'da tutabiliriz.

- Artıları:
  - Ekonomik ve kablosuz.
- Eksileri:
  - Bu iki cihaz aynı kanalı kullanmakta (çoğu zaman). Bu sebeple iki access point ile kurulan bu uzatmada iki cihazın birbirine ulaşması için 3 kez yayın durdurulmak durumundadır. (Cihaz -> AP, AP -> Diğer AP, Diğer AP -> Diğer Cihaz) Kullanılmaz denemez fakat gecikmeye yol açmaktadır.

### UTP Kablo ile uzatma
- Artıları:
  - Doğrudan kablo ile en iyi performansı almış oluyoruz.
- Eksileri:
  - Kablo fazlalığı ve dağınık görünüm.

### HomePlug ile uzatma
Şebekeden gelen elektrik vasıtasıyla çalışan aparatlarla routerdan gelen bağlantının şebekeye verilmesi ve diğer odadan aynı aparatla alınıp cihaza getirilmesidir.

- Artıları:
  - Daha temiz görünmektedir.
- Eksileri:
  - Piyasada çok ucuz olanları şebeke elektriğindeki dalgalanmalar yüzünden kolayca bozulabildiğinden; biraz tuzlu olabilmektedir.