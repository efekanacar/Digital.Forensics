### Linux Incident Response

## Linux Dosya Dizin Sistemi
/ (kök)
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var



-   `/` (kök): Dosya sisteminin en üst düzeyidir. Tüm diğer dizinleri içerir.
-   `/bin`: İkili (binary) dosyaların bulunduğu dizin. Önemli sistem programları burada bulunur.
-   `/boot`: Başlatma (boot) süreciyle ilgili dosyaları içeren dizin. Önyükleme yöneticisi (bootloader) burada bulunur.
-   `/dev`: Aygıtların dosya temsillerini içeren dizin. Donanım bileşenlerine ilişkin dosyalar burada bulunur.
-   `/etc`: Sistem yapılandırma dosyalarının bulunduğu dizin. Ağ yapılandırması, kullanıcı hesapları ve diğer sistem ayarları burada yer alır.
-   `/home`: Kullanıcıların ev dizinlerinin bulunduğu dizin. Her kullanıcı burada kendi kişisel dosyalarını tutar.
-   `/lib`: Paylaşılan kitaplık dosyalarını (library) içeren dizin. Programlar tarafından kullanılan ortak kütüphaneler burada bulunur.
-   `/media`: Taşınabilir ortamların (USB sürücüler, CD/DVD sürücüler vb.) otomatik olarak bağlandığı dizin.
-   `/mnt`: Geçici olarak bağlanan dosya sistemlerinin (diskler, ağ paylaşımları vb.) bulunduğu dizin.
-   `/opt`: Üçüncü taraf yazılımların kurulu olduğu dizin. Genellikle sistemle birlikte gelmeyen yazılımlar buraya yerleştirilir.
-   `/proc`: İşlem bilgilerini içeren sanal bir dosya sistemi. Sistem ve işlem bilgileri buradan okunabilir.
-   `/root`: Süper kullanıcı (root) için ev dizini. Root kullanıcısının kişisel dosyaları burada bulunur.
-   `/run`: Çalışma zamanı verilerini tutan geçici bir dosya sistemi. Örneğin, sistem başlatıldığında çalışan servisler burada bilgi saklar.
-   `/sbin`: Sistem yönetimi ile ilgili ikili dosyaların bulunduğu dizin. Özel yetkilere sahip kullanıcılar tarafından kullanılır.
-   `/srv`: Sistem tarafından sunulan hizmetlerin (services) dosyalarını içeren dizin.
-   `/sys`: Linux çekirdeği ve sistem bileşenlerinin bilgilerini tutan sanal bir dosya sistemidir.
-   `/tmp`: Geçici dosyaların tutulduğu dizin. Her oturumda temizlenir.
-   `/usr`: İkincil kullanıcıların ve paylaşılan programların dosyalarını içeren büyük bir dizin. Uygulama ve kütüphane dosyaları burada yer alır.
-   `/var`: Değişken verilerin tutulduğu dizin. Log dosyaları, veritabanları ve diğer değişken veriler burada bulunur.

## Log Dosyaları ve Log Analizi
Log dosyaları, sistem ve uygulamalar tarafından oluşturulan olayların kaydedildiği metin dosyalarıdır. Bu dosyalar, sistem durumu, hata mesajları, güvenlik olayları ve diğer önemli bilgileri içerebilir. Log dosyaları, sorun giderme, performans analizi ve güvenlik denetimleri gibi bir dizi amaç için kullanılır.

Log analizi, log dosyalarının incelenmesi ve anlamlandırılması sürecidir. Bu analiz, sistem durumunu izleme, hataları tespit etme, saldırıları tespit etme ve genel sistem performansını değerlendirme gibi çeşitli hedeflere yönelik olabilir. Log analizi, bilgisayar güvenliği, sistem yönetimi ve ağ izleme gibi alanlarda yaygın olarak kullanılır.

Log analizi genellikle aşağıdaki adımları içerir:

1.  Log dosyalarının toplanması: Sistem ve uygulamalar tarafından oluşturulan log dosyaları toplanır ve bir merkezi kayıt noktasında depolanır.
2.  Log dosyalarının filtrelenmesi: İlgilenilen olayları içeren log kayıtları seçilir ve gereksiz bilgiler elenir.
3.  Log dosyalarının indekslenmesi: Log dosyaları hızlı erişim için indekslenir, böylece belirli olayları aramak ve filtrelemek daha kolay hale gelir.
4.  Log dosyalarının analizi: Log kayıtları analiz edilir ve önemli olaylar, hatalar, saldırı girişimleri vb. belirlenir.
5.  Log dosyalarının raporlanması: Analiz sonuçları raporlar halinde sunulur ve gerektiğinde ilgili kişilere bildirilir.
6.  Olayları izleme ve tepki: Belirli olayları izlemek ve gerektiğinde tepki vermek için otomatik uyarılar ve tetiklemeler kurulabilir.

## Olay Müdahalesi
Olay Müdahalesi, bir bilgisayar veya ağ güvenliği olayı meydana geldiğinde gerçekleştirilen bir eylem planı olarak
tanımlanabilir. Bir Olay Müdahale Uzmanı olarak sistemlerinizde nelerin bulunması ve nelerin olmaması gerektiğinin
her zaman farkında olmalısınız.

# /etc/passwd
Sisteminizde şüpheli görünebilecek bir hesap girişi olup olmadığını tespit etmek. Bu komut genellikle kullanıcı hesabıyla
ilgili tüm bilgileri getirir. 
*cat /etc/passwd*

# passwd -S
Linux'taki 'Setuid' seçeneği benzersiz dosya iznidir. Yani bir Linux sisteminde kullanıcı şifre değişikliği yapmak
istediğinde 'passwd' komutunu çalıştırabilir . Root hesap setuid olarak işaretlendiğinden geçici izin alabilirsiniz.
*passwd -S raj* 

# grep
Grep , normal ifadeyle eşleşen satırları düz metinde aramak için kullanılır . :0: /etc/passwd dosyasındaki 'UID 0'
dosyalarını görüntülemek için kullanılır .
*grep :0: /etc/passwd*

# find / -nouser
Bir saldırganın saldırı gerçekleştirmek üzere herhangi bir geçici kullanıcı oluşturup oluşturmadığını belirlemek ve görüntülemek için şunu yazın:
*find / -nouser -print*

# /etc/shadow
/etc/shadow dosyası şifrelenmiş parolayı ve parolalarla ilgili ayrıntıları içerir ve yalnızca kök
kullanıcılar tarafından erişilebilir.
*cat /etc/shadow*

# /etc/group
Grup dosyası, kullanıcı tarafından kullanılan grupların bilgilerini görüntüler. Ayrıntıları görüntülemek için yazın
*cat /etc/group*

# /etc/sudoers
Görüntülenecek kullanıcı ve grup ayrıcalıkları hakkındaki bilgileri görüntülemek istiyorsanız/etc/sudoers
dosyası görüntülenebilir
*cat /etc/sudoers*

# lastlog
Belirli bir kullanıcının veya Linux sistemindeki tüm kullanıcıların en son oturum açma raporlarını görüntülemek için
şunu yazabilirsiniz:
*lastlog* 

# auth log
Sistemdeki meraklı SSH ve telnet oturum açma bilgilerini veya kimlik doğrulamasını belirlemek için /var/log/ dizinine
gidip şunu yazabilirsiniz:
*tail auth.log*

# history
Kullanıcının yazdığı komutların geçmişini görüntülemek için, daha az komutla geçmiş yazabilir veya en
son yazdığınız komut sayısından bahsedebilirsiniz. Geçmişi görüntülemek için yazabilirsiniz
*history | less*

# uptime
Linux sisteminizin fazla mesai yapıp yapmadığını öğrenmek veya sunucunun ne kadar süredir çalıştığını,
sistemdeki geçerli saati, kaç kullanıcının oturum açtığını ve sistemin yük ortalamalarını görmek için şunu
yazabilirsiniz:
*uptime* 

# free
Linux'ta sistemin bellek kullanımını, sistemde kullanılan fiziksel ve swap belleğin yanı sıra çekirdek tarafından
kullanılan arabellekleri görüntülemek için şunu yazabilirsiniz:
*free*

# /proc/meminfo
Sistemdeki koçun, mevcut bellek alanının, arabelleklerin ve takasın ayrıntılı bilgilerini kontrol etmek için
olay müdahale görevlisi olarak şunu yazabilirsiniz:
*cat /proc/meminfo* 

# /proc/mounts
Bir olay müdahale görevlisi olarak, sisteminizde bilinmeyen bir bağlantı olup olmadığını kontrol etmek sizin
sorumluluğunuzdadır; sisteminizde mevcut olan bağlantıyı kontrol etmek için şunu yazabilirsiniz:
*cat /proc/mounts* 

# top
Linux sisteminde çalışan tüm süreçlerin dinamik ve gerçek zamanlı görselini, sistem bilgilerinin özetini ve süreçlerin listesini
ve Linux Çekirdeği tarafından yönetilen ID numaralarını veya thread'leri elde etmek için, Linux Çekirdeği tarafından yönetilen
işlemlerden yararlanabilirsiniz.
*top* 

# ps aux
Linux'unuzun işlem durumunu ve şu anda çalışan işlem sistemini ve PID'yi görmek için. Linux sistemindeki herhangi bir kötü niyetli etkinliği
gösterebilecek anormal süreçleri belirlemek için şunları yapabilirsiniz:
*ps aux*

# PID
Belirli bir işlem hakkında daha fazla ayrıntı görüntülemek için şunu kullanabilirsiniz:
*lsof -p [pid]*

# service
Anormal şekilde çalışan hizmetleri bulmak için şunları kullanabilirsiniz:
*service --status-all*

# /etc/cronjob
Olaya müdahale eden kişi, şüpheli planlanmış görevleri ve işleri aramalıdır . Zamanlanmış görevleri bulmak için şunları kullanabilirsiniz:
*cat /etc/cronjob*

# /etc/resolv.conf
DNS yapılandırma sorunlarını çözmek ve çeşitli çözümleyici bilgileri sağlayan değerleri içeren bir anahtar kelime listesinden yararlanmak için şunu kullanabilirsiniz:
*more /etc/resolv.conf*

# /etc/hosts
Web sitesinde veya SSL kurulumunda yapılan değişiklikleri test etmek için yararlı olan, ana bilgisayar adlarını veya alan adlarını IP
adreslerine çeviren dosyayı kontrol etmek için şunu kullanabilirsiniz:
*more /etc/hosts*

# iptables
Linux sistemlerinde IPv4 paket filtrelemeyi ve NAT'ı kontrol etmek ve yönetmek için iptables'ı kullanabilir ve aşağıdaki gibi
çeşitli komutlardan yararlanabilirsiniz:
*iptables -L -n*

# büyük dosyalar
Sisteminizdeki aşırı büyük dosyaları ve bunların izinlerini hedefleriyle birlikte tanımlamak için şunları yapabilirsiniz:
*find /home/ -type f -size +512k -exec ls -lh {} \;*

# mtime
Olay müdahale görevlisi olarak 2 gündür sistemde bulunan anormal bir dosyayı görmek istiyorsanız şu komutu kullanabilirsiniz:
*find / -mtime -2 -ls* 

# ifconfig
Ağ etkinliği bilgilerini elde etmek için çeşitli komutları kullanabilirsiniz.
Tüm ağ arayüzlerini görmek için kullanabilirsiniz.
*ifconfig -a*

# dosyaları aç
Bağlantı noktalarını dinleyen tüm işlemleri PID'leriyle listelemek için kullanabilirsiniz.
*lsof -i*

# netstat
Ağ kullanımındaki tüm dinleme bağlantı noktalarını görüntülemek için
*netstat -nap*

# arp
Sistem ARP önbelleğini görüntülemek için şunu yazabilirsiniz:
*arp -a*

# PATH
$PATH, kullanabileceğiniz yolunuzda bulunan dizinleri kontrol etmek için kabuğa yürütülebilir dosyaları hangi dizinlerde arayacağını
söyleyen bir dizin listesi görüntüler.
*echo $PATH*


