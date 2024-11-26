Çok kullanılmayan Linux Komutları
İster Sistem Yöneticisi, Geliştirici, DevOps, Güvenlik veya Operasyon uzmanı olun, Linux'u ve araçlarını etkili bir şekilde kullanmak öğrenebileceğiniz en temel beceridir. Linux, dünyadaki sunucuların ve uygulamaların çoğunluğunun temelini oluşturur.
"Profesyonel geliştiricilerin %47'si Linux tabanlı işletim sistemleri kullanmaktadır."
## Linux Komutları: Herkesin kullandığı
Bunların çoğu ls veya echo gibi komutları gösteren başlangıç seviyesinde, sanırım çoğunuz temel komutları zaten biliyorsunuz.
Bu makale farklı. İş yerinde her gün kullandığım komutların kişisel bir özetini paylaşacağım. Bu liste başlangıç ipuçlarının ötesine geçiyor ve daha hızlı çalışmanıza ve Linux'u daha iyi yönetmenize yardımcı olacak komutlara odaklanıyor.
İki bölümden oluşacak:
1. Linux Araçları - Önemli araçlar ve bunları etkili kullanma
2. Geçici Komutlar - İhtiyaç duyduğunuzda hızlı çözümler için kullanışlı komutlar
## Linux Araçları
### Yardımcı Programlar
#### rsync
Dosya ve dizinleri hedefe kopyalamak için kullanılır, cp komutuna benzer. Ancak uzak konumlara kopyalama yapabilir ve ilerleme çubuğu gösterebilir, genellikle yedeklemeler için kullanılır.
```bash
# Örnek Kullanım
$ rsync -vap - ignore-existing <kaynak_dosya> <hedef_dosya>
# Önemli bayraklar:
v = ayrıntılı, r = özyinelemeli, p = izinleri koru, g = grup, o = sahip, a = arşiv, - progress = ilerleme çubuğu
```
#### mkpasswd
mkpasswd basit ama çok kullanışlı bir komuttur, belirtilen uzunlukta karmaşık rastgele şifre oluşturur.
```bash
$ mkpasswd -l 8
> iwF1g2Lo
```
#### screen
Screen tam ekran pencere yöneticisidir; içinde kabuk çalıştıran tek bir pencere oluşturur ve tek bir oturum içinde birden fazla screen penceresinin çalışmasına izin verir. Uzaktan uzun bir görev çalıştırıyorsanız ve SSH oturumunuzun düşüp her şeyi mahvetmesinden endişeleniyorsanız çok faydalıdır. Screen bağlantı kesintisinden sonra da çalışmaya devam eder.
```bash
# Örnek Kullanım
$ screen # Screen oturumu başlat
$ screen -ls # Çalışan servisleri listele
$ screen -r # Oturuma bağlan
```
Makalenin devamını Türkçe çevirisiyle sunuyorum:
#### Ldapsearch
LDAP veritabanlarıyla düzenli olarak çalışıyorsanız, Ldapsearch olmazsa olmazdır. Bu araç, LDAP sunucusuna bağlantı açar ve veritabanınızdaki girişleri aramanıza, bulmanıza ve hata ayıklamanıza olanak tanır.
```bash
# Örnek Kullanım
$ ldapsearch -x -W -D <kullanıcı_adı> | less
# Önemli Bayraklar
-x = basit kimlik doğrulama
-W = şifre sorma
-D = LDAP dizinine bağlanmak için ayırt edici binddn adını kullan
```
### İzleme Araçları
#### Uptime
Uptime, bir sunucunun ne kadar süredir çalıştığı, mevcut zaman, kullanıcı sayısı ve bellek kullanım ortalamaları gibi metrikleri döndürür. Sunucunuzda bir şeyler ters gittiğinde, genellikle ilk başvurulan komuttur.
#### w
Evet, tek harf. Bu, uptime ve who komutlarının harika bir kombinasyonudur.
```bash
$ w
```
#### Wall
Wall, herhangi bir sistem yöneticisi için kullanışlı bir komuttur; sistemde o anda oturum açmış olan herkesin terminaline mesaj göndermenizi sağlar. Bu, sistem genelindeki duyurular için çok kullanışlı olabilir.
```bash
$ wall "Bakım 13:30'da planlanmıştır"
```
#### Top
CPU ve kritik bellek kullanımı ile CPU kullanım metrikleri için otomatik yenilenen bir süreç listesi gösterir.
```bash
$ top
```
#### Ncdu
ncdu komutu, disk kullanımı için hızlı ve kullanışlı bir görünüm sağlar. En çok disk alanı kullanan dizinleri hızlı ve kolay bir şekilde görmek için kullanabilirsiniz.
```bash
$ ncdu
```
#### lsof
lsof, temel bir amaç için kullanılan tek bir komuttur: Açık Dosyaları Listele (LiSt Open Files). Özellikle dosyaların kullanımda olduğunu söyleyen bağlama sorunları yaşarken çok kullanışlıdır. Bu komut, hangi dosyaların hangi işlemler tarafından kullanıldığını hızlıca tanımlar.
```bash
$ lsof
```
### Ağ Araçları
#### Netcat
Netcat veya nc öncelikle port taraması için kullanılır, ancak aslında sistem yöneticilerinin herhangi bir görev için ellerinin altında bulundurmaları gereken harika bir ağ yardımcı programıdır. Netcat; port tarama, dosya kopyalama, port yönlendirme, proxy sunucuları ve sunucu barındırma gibi işlemleri destekleyebilir… Kısacası inanılmaz derecede çok yönlüdür.
```bash
# Örnek Kullanım:
$ nc -vz <host> <port> # İki host arasındaki bağlantıyı belirli bir portta kontrol eder
$ nc -l 8080 | nc <host> 80 # Proxy sunucu oluşturma
```
#### NetStat
Netstat; yönlendirme tabloları, ağ bağlantıları, üyelikler, istatistikler, bayraklar vb. gibi çeşitli ağ ayrıntılarını döndürür.
```bash
# Örnek Kullanım 
$ netstat -a # Tüm ağ portlarını listele
$ netstat -tlpn # Tüm dinleme portlarını listele
# Önemli Bayraklar
-s = İstatistikleri göster
-v = Ayrıntılı
-r = Yönlendirme tablolarını göster
-i = Arayüz tablosunu göster
-g = Grup üyeliklerini göster
```
#### Nslookup
İnternet veya yerel ağınızdaki sunucular hakkında bilgi almak için kullanılır. Ad sunucusu bilgilerini bulmak için DNS'yi sorgular ve ağ hata ayıklama için kullanışlı olabilir.
```bash
# Örnek Kullanım
$ nslookup medium.com/tags/devops
# Önemli Bayraklar
-port = Bağlantı için port numarasını değiştir
-type = Sorgu türünü değiştir
-domain = Arama listesini isme ayarlar
```
#### TCPDump
Sisteminize gelen ve giden trafiği yakalamak ve analiz etmek için kullanılır. Ağ sorunlarının hata ayıklaması ve giderilmesinde uzmanlaşmış, güçlü ve çok yönlü bir araçtır, aynı zamanda bir güvenlik aracı olarak da kullanılabilir.
```bash
# Örnek Kullanım
$ tcpdump
$ tcpdump -i <arayüz> <ip_adresi veya hostname> <port>
```
### Geçici Komutlar
#### API Yanıtlarını Güzel Yazdırma
API'lerle çalışırken terminalde JSON verilerini okumak oldukça sinir bozucu olabilir. Aşağıda görebileceğiniz gibi, küçük bir veri kümesi bile komut satırında görüntülendiğinde hızlıca karışıklığa dönüşüp okunması çok zor hale gelebilir.
```bash
$ cat test.json
{"title":"Person","type":"object","properties":{"firstName":{"type":"string"},"lastName":{"type":"string"},"age":{"description":"Age in years","type":"integer","minimum":0}},"required":["firstName","lastName"]}
```
Neyse ki Python'un bir çözümü var. Çıktınızı python'a yönlendirerek JSON tool modülünü çağırabiliriz. Bu, JSON belgesini çok daha kolay okunabilir ve göze daha hoş görünen bir şekilde yazdıracaktır.
[Güzel formatlanmış JSON örneği…]
Ayrıca, komut satırı JSON arayüzü olan JQ'yu da referans göstermek gerekir:
```bash
$ jq . file.json
```
#### Kullanılabilir Paketleri apt ile Arama
```bash
$ apt-cache search <anahtar_kelime>
```
#### İki Komutun Çıktısını Karşılaştırma
```bash
# İki ls komutunun çıktısını karşılaştırma örneği
$ diff -u <(ls -l /dizin/) <(ls -l /dizin/) | colordiff
```
#### Unix Zaman Damgasını İnsan Tarafından Okunabilir Formata Dönüştürme
```bash
# Unix zaman damgasını insan tarafından okunabilir formata dönüştür
$ date -d 1656685875
Fri, 01 Jul 2022 14:31:15 +0000
# Mevcut zamanı UNIX zaman damgası olarak al
$ date "+%s"
```
#### Git Commit'lerini Birleştirme
```bash
$ git log # Kaç commit yaptığınızı görün
$ git rebase -i HEAD~x # x = yaptığınız commit sayısı
# Metin editöründe değişiklikleri yapın, son commit'i pick olarak tutun ve diğerlerini squash olarak değiştirin
# Commit mesajlarını düzenleyin, tercihen önceki commit'lerden olanları kaldırın
$ git push - force-with-lease
```
#### Tüm Systemd Servislerini Listeleme
```bash
$ systemctl -l -t service | less
```
