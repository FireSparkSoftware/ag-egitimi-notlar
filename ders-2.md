# WIFI Eğitimi 2. Ders Notları

# Güvenlik Saldırıları

## Man in the middle (aradaki adam)
A ile B arasında haberleştiğimizi düşünelim. A ile B arasına üçüncü bir şahısın girip tüm trafiği dinlemesi man in the middle saldırısı denir.

## DoS (Deny of Service)
Wireless'ın çalıştığı frekanstan, daha güçlü bir yayın yapılırsa var olan yayını bastırarak sistem devre dışı kalabilir. Tüm cihazların kablosuz haberleştiği bir fabrikada bu durum sakıncalıdır.

# Güvenlik Çözümleri

## Benzersiz SSID ve Gizli Ağ
AP'lerimiz bizim ağın adını görebilmemiz için her 100ms'de `beacon` denen frameler yollamaktadır. Güvenlik konusunda da ağımızı gizleyebilir yani bu `beacon frame`leri yollatmayabiliriz.

Gizlenen ağlara bağlanabilmemiz için cihazımız `ProbeRequest` atmaktadır. Bu da ilgili AP'e "bana bilgilerini gönder" demek olmakta. Yani gizlenmiş bir SSID'ye sahip ağa bağlanmak istediğinizde AP size mutlaka SSID bilgisi dönmektedir. Bu nedenle pek etkili bir korunma yöntemi değildir.

## MAC Tabanlı Doğrulama
Her kartın bir MAC adresi vardır ve eşsizdir. Bağlanacağımız AP'e sadece izin verilen MAC adreslerini girerek başka cihazların bağlanmasını engellemiş oluruz.

Fakat durum şu ki, var olan bağlantı bir yayın yapmaktadır. Nasıl ki bir radyo yayınında 100MHz ile PowerFM dinleyebiliyorsak doğru kanalı dinleyen insanlar da ağ üzerindeki trafiği dinlemiş olurlar. Bu durumda ağda iletişim halindeki MAC adreslerimizi öğrenmiş olurlar ve kendi MAC adreslerini değiştirip ağa dahil olabilirler.

## WEP Şifreleme (Wired Equivalent Privacy)
RC4 algoritması (Rivest Cipher 4) ile şifreleme yapmaktaydı. RC4 algoritması çok önceden kırılmış bir algoritmaydı fakat Wireless için bunu tercih etmişlerdi. Sebebi de muhtemelen o zamanın bilgisayarlarının güçleri daha iyi bir algoritma için yeterli olmamasıydı.

Anahtar boyu 40 bit + Başlangıç vektörü (IV) 24 bit = 64 bitlik bir şifreleme yapmaktaydı. Asıl anahtarın boyu 40 bitti. İçine 24 bitlik bir rastlansal küme ekleniyordu. Fakat bu 24 bitlik anahtar karşı tarafa yollanan paketin içinde ve açık bir şekilde gidiyordu. 40 bitlik anahtar hiç değiştirilmiyordu ve güvenlik böyle sağlanıyordu.

### 128 Bit Standart dışı WEP
104 bit anahtar + 24 bit başlangıç vektörü (IV) = 128 bitlik bir anahtar ile şifreleniyordu ve şifrenin daha zor kırılacağı düşünülüyordu.

### WEP Zayıflıkları
IV (başlangıç vektörü) lerin tekrar kullanılması: 2^24 = yaklaşık 17 milyon farklı IV oluşturulabiliyor. IEEE 802.11b 500 frame/saniye için yaklaşık 7 saatte tüm IV uzayı kullanıldığından dolayı zaman içerisinde aynı anahtarlar oluşabilmekteydi. Bu da kırılmasına yol açmaktaydı.

## WPA-1 (Wi-Fi Protected Access)
Endüstrinin acil ihtiyacı için IEEE'nin standartlandırılma çalışmalarını beklemeden sektör kendisi için 802.11i standartlarına (draft 3.0) uygun geçici bit güvenlik sistemi oluşturuldu. (Wi-Fi tarafından) RC4 kullanır, TKIP protokolü ile anahtar sürekli değiştirilir.

## WPA-2
802.11i standartı ile beraber AES kriptosuna geçilir. AES yapısı gereği anahtarı sürekli değiştirmektedir.

# Kimlik denetimi?
WPA-1/WPA-2 kimlik denetimi yapmaz, kriptolanmayı gerçekleştirir. Sonradan eklenebilir.

Kimlik denetimi için:
- OPEN: Kimlik denetimi yapılmayacak.
- SHARED: WEP anahtarı ile kimlik denetimi yapar fakat kötü bir çözümdür ve günümüzde kullanılmaz.
- EAP (Extensible Authentication Protocol) (802.1x ile beraber): Yerel alan ağında kimlik denetimi yapılması için geliştirilen bir ek protokoldür. Wireless ve Ethernet için geçerlidir. Kullanıcı adı ve şifrenin güvenli bir şekilde merkeze götürülebilmesi için geliştirilmiş protokol ailesidir.

Haberleşmenin kriptolanması ile karıştırılmamalıdır. Kullanıcı adı ve şifrenin kriptolu bir şekilde AP'ye ulaştırmak için EAP protokolü kullanılıyor.

## WPA-Enterprise
Kurumsal ağlarda kullanılır. Kendimize ait bir sertifikaya ihtiyacımız var. Private ve Public keyler ile çalışan hayli güvenli bir mimaridir. Sertifika da Public Key'i içeren bir metin dosyasıdır. Hem altyapı hem de istemci kimlik denetiminden geçer. Her kullanıcı bağlandığı anda master key yeniden türetilir. Bu master key haberleşme sırasında sürekli tekrar üretilir.

TLS/SSL kullanan HTTPS servisleri için; nasıl ki biz bir sayfaya gittiğimizde "karşımızdaki sayfa gerçekten gitmek istediğimiz sayfa mı?" doğrulaması yaptığımız gibi, bu doğrulama mimarisi Wireless ağlarda da geçerlidir. Biz netowrk'e bağlandığımızda "bu AP gerçekten bağlanmak istediğimiz AP mi?" sorgusu sertifikalar yardımıyla yapılmakta. Biz karşıdaki AP'yi doğrulamadıkça kimlik bilgilerimizi karşıdaki AP ile paylaşmıyoruz. EAP protokollerini kullanarak arkadaki RADIUS sunucusu ile haberleşiyoruz.

## Eduroam
Eduroam bir SSID adıdır. Eğitim kurumlarındaki personel ve öğrenciler için başka bir kurumda o kuruma özel bir kullanıcı adı ve parola olmadan kendi kimlik bilgileriyle de Eduroam ağına bağlanabilmeleri için geliştirilmiş sistemdir. Kurumlar arası RADIUS sunucuları iletişim halinde olur.

# Güvenlik Açıkları

## WPS (Wi-Fi Protected Setup) Brute-Force Attack
Cihazın daha kolay ağa katılabilmesi için geliştirilmiş bir sistem. İlk nesillerde bu özellikte güvenlik açıkları tespit edildi ve yeni nesil cihazlarda bu açık kapatıldı. Yine de bu özelliği kapalı tutmakta fayda var.