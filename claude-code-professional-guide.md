# Claude Code'u Profesyonel ve Verimli Kullanma Rehberi

> Yazılım ekipleri ve bireysel geliştiriciler için uygulamalı rehber.
> Sürüm 1.0 · 28 Eylül 2026

UYGULAMALI REHBER

Claude Code'u Profesyonel ve Verimli Kullanma Rehberi

Yazılım ekipleri ve bireysel geliştiriciler için

Sürüm 1.0 · 28 Eylül 2026

Resmî Claude Code dokümantasyonu esas alınmıştır

Claude Code, yalnızca kod öneren bir sohbet aracı değil; proje
dosyalarını okuyabilen, terminal komutları çalıştırabilen, dosya
düzenleyebilen ve testleri yürütebilen bir kodlama ajanıdır. En iyi
sonuç, onu "benim yerime kod yaz" diyerek serbest bırakmakla değil;
hedefi, çalışma sınırlarını ve başarı ölçütünü açıkça tanımlayıp
çıktısını doğrulamakla alınır. Bu rehber, Claude Code'u araştırma,
planlama, uygulama, doğrulama ve inceleme süreçlerinde kontrollü bir
geliştirme ajanı olarak kullanmak için uygulamalı bir çerçeve sunar.

## Beş temel ilke

## İçindekiler

1.  Temel çalışma modeli

2.  İşe göre doğru yaklaşım

3.  Profesyonel günlük akış

4.  Kullanıma hazır prompt şablonları

5.  CLAUDE.md ile kalıcı proje bağlamı

6.  Uzantılar: hangi ihtiyaçta hangi araç?

7.  Güvenlik ve izinler

8.  Bağlam ve maliyet yönetimi

9.  Takımda ölçeklendirme

10. Sık yapılan hatalar

--- Hızlı başlangıç kontrol listesi

--- Sonuç

--- Ek A --- Kopyala-yapıştır görev şablonu

--- Kaynaklar

# 1. Temel çalışma modeli

İyi bir Claude Code isteği beş unsuru netleştirir. Bu unsurlar ne kadar
somutsa, ardışık düzeltme turları o kadar azalır. \[1\]

Örneğin "giriş sorununu düzelt" yerine şunu yazın:

Bilinen dosya yollarını @src/auth/session.ts gibi doğrudan belirtin.
Yolu bilmiyorsanız önce Claude'dan kod tabanını keşfetmesini isteyin.

## Çalışma döngüsü

Profesyonel kullanımda her değişiklik ölçülebilir bir kabul kriterine
bağlanır. Güvenilir döngü altı adımdan oluşur:

Her adım her işte gerekmez; hangilerinin gerektiğini işin belirsizliği
ve riski belirler (Bölüm 2). Döngünün günlük uygulaması Bölüm 3'te adım
adım anlatılır.

# 2. İşe göre doğru yaklaşım

Her göreve aynı süreçle yaklaşmak ya küçük işleri gereksiz yere
yavaşlatır ya da büyük işleri riske atar. \[1\]

## Plan modunu doğru kullanın

Plan modunda Claude dosyaları okur, keşif için komut çalıştırır ve bir
plan yazar; siz planı onaylayana kadar kaynak kodu düzenlemez. Oturumu
plan modunda başlatmak için: \[2\] \[5\]

Oturum içinde Shift+Tab ile modlar arasında geçebilir ya da tek bir
isteğin başına /plan yazabilirsiniz. Plan hazır olduğunda Ctrl+G ile
planı metin editörünüzde açıp doğrudan düzenleyebilirsiniz.

# 3. Profesyonel günlük akış

Bu bölüm, Bölüm 1'deki altı adımlı çalışma döngüsünü günlük pratiğe
çevirir. Her adım başlığında döngüdeki karşılığı parantez içinde
belirtilmiştir; Adım 1 döngü başlamadan önceki hazırlıktır.

## Adım 1 --- Çalışma alanını hazırlayın (hazırlık)

Proje kökünde başlayın ve mevcut durumu görün:

Çalışma ağacında size ait değişiklikler varsa Claude'dan bunları
korumasını açıkça isteyin. Birbirinden bağımsız, paralel işler için her
oturuma ayrı bir Git worktree verin:

Bu komut .claude/worktrees/ altında ayrı bir dizin ve dal oluşturur;
böylece paralel oturumların dosya değişiklikleri çakışmaz. Yeni worktree
uzak depodaki varsayılan dalı temel alır; commit edilmemiş yerel
değişiklikleriniz oraya taşınmaz. \[2\]

## Adım 2 --- Önce mevcut davranışı anlatmasını isteyin (01 Keşfet)

Hata düzeltme ve yeni özelliklerde Claude'dan önce ilgili kod yolunu ve
var olan testleri özetlemesini isteyin. Hata için yeniden üretme
adımlarını ve tam hata çıktısını paylaşın. Emin değilseniz "henüz dosya
değiştirme; önce bulguları raporla" diyerek keşfi salt okunur tutun.

## Adım 3 --- Kabul kriterini birlikte netleştirin (02 Planla)

Büyük özelliklerde Claude'dan açık sorular sormasını, kenar durumları ve
ödünleşimleri netleştirmesini isteyin. Ardından kısa bir teknik taslak
hazırlatın: değişecek dosyalar, arayüzler, kapsam dışı maddeler ve son
doğrulama adımı. Böylece uygulama sırasında farklı varsayımlarla
ilerlenmez.

## Adım 4 --- Küçük adımlar, yakın geri bildirim (03 Uygula)

İşi test edilebilir parçalara bölün. Yön yanlışsa Esc ile durdurup hemen
düzeltin. Riskli bir denemeden dönmek için /rewind kullanabilirsiniz
(bkz. Bölüm 8); yine de Git'i asıl geri dönüş mekanizması olarak
koruyun. Aynı sorunda tekrar tekrar düzeltme yapıyorsanız,
öğrendiklerinizi içeren net bir istekle temiz bir oturum başlatmak
genellikle daha hızlıdır.

## Adım 5 --- Doğrulamayı işin parçası yapın (04 Doğrula)

Claude, çalışmasını doğrulayabildiğinde belirgin biçimde daha iyi sonuç
verir. Hangi kontrollerin çalışacağını isteğin içinde söyleyin; önce en
ilgili ve hızlı testi, gerektiğinde daha geniş kontrolleri çalıştırtın:
\[1\]

Davranış değişikliğini kapsayan birim veya entegrasyon testi

Lint ve tür kontrolü; gerekiyorsa production build

API değişikliklerinde örnek istek ve yanıt

Arayüz değişikliklerinde uygulamayı çalıştırıp ekran görüntüsüyle
tasarım karşılaştırması

Migration işlerinde dry-run, test verisi ve geri alma planı

Sonuç raporunda çalıştırılan komutları, başarılı/başarısız durumları ve
çözülmemiş riskleri isteyin. "Bitti" demesi tek başına doğrulama
değildir.

## Adım 6 --- Gözden geçirin ve teslim edin (05 İncele · 06 Kaydet)

Claude'dan diff'i özetlemesini, kapsam dışı değişiklik olup olmadığını
kontrol etmesini ve test kanıtlarını göstermesini isteyin. Kritik
değişikliklerde kodu yazan oturumdan bağımsız bir inceleme yaptırın:
yeni bir oturum ya da ayrı bir alt ajan. Git diff'ini ve kritik alanları
kendiniz de gözden geçirin. Küçük, açıklayıcı commit'ler oluşturun (ör.
Conventional Commits); ana dala doğrudan push yapmayın.

# 4. Kullanıma hazır prompt şablonları

Köşeli parantezli alanları kendi bağlamınızla doldurun. Şablonlar Bölüm
1'deki beş unsuru içerecek şekilde tasarlanmıştır. Kapsamlı genel görev
şablonu için Ek A'ya bakın.

## Hata düzeltme

## Yeni özellik (önce plan)

## Refaktör

## Kod tabanını tanıma

## Alt ajanla araştırma

## Bağımsız kod incelemesi

## Teslim öncesi kontrol

# 5. CLAUDE.md ile kalıcı proje bağlamı

CLAUDE.md her oturumda yüklenen proje talimatlarını taşır. Başlangıç
için proje kökünde /init çalıştırıp üretilen taslağı inceleyin; ardından
/memory ile hangi talimat dosyalarının yüklendiğini kontrol edin. Resmî
dokümantasyon, CLAUDE.md dosyası başına 200 satırın altını hedeflemeyi
öneriyor; uzun dosyalar daha fazla bağlam tüketir ve talimatlara uyumu
azaltabilir. \[3\]

## Örnek CLAUDE.md

## Bakım ilkeleri

Aynı düzeltmeyi iki kez yapmak zorunda kaldıysanız veya kod
incelemesinde Claude'un bilmesi gereken bir eksik çıktıysa, kuralı
CLAUDE.md'ye ya da uygun kapsamlı kurala ekleyin.

Büyüyen talimatları .claude/rules/ altında yol kapsamlı kurallara bölün;
bu kurallar yalnızca Claude eşleşen dosyalarla çalışırken yüklenir.
\[3\]

Birbiriyle çelişen kurallarda Claude birini keyfi seçebilir; CLAUDE.md,
alt dizin dosyaları ve kuralları düzenli olarak gözden geçirin.

Talimatlar rehberlik sağlar, teknik olarak zorlayıcı bir güvenlik sınırı
değildir. Bir eylemi kesin olarak engellemek için izin (deny) kuralı
veya hook kullanın. \[3\] \[10\]

# 6. Uzantılar: hangi ihtiyaçta hangi araç?

Başlangıçta bütün uzantıları kurmak yerine temel bağlamdan başlayın ve
tekrar eden bir sorun ortaya çıktıkça doğru aracı ekleyin. \[8\] \[9\]
\[10\] \[11\]

Basit seçim kuralı

Bilgi her zaman mı gerekli? → CLAUDE.md

Prosedür ara sıra mı gerekiyor? → Skill

Her koşulda otomatik mi çalışmalı? → Hook

Başka bir sistemle mi konuşmalı? → MCP

İş ana konuşmayı mı kirletiyor? → Alt ajan

Güvenmediğiniz MCP sunucularını bağlamayın; harici içerik prompt
injection riski taşıyabilir. Alt ajanlara yalnızca gereken araçları ve
kapsamı verin; izinleri ve maliyetleri ayrıca değerlendirin. \[6\]
\[11\]

# 7. Güvenlik ve izinler

Claude Code dosyaları okuyabilir, terminal komutları çalıştırabilir ve
dış araçlara erişebilir. Bu nedenle izin ekranlarını tıklayıp geçilecek
bir engel olarak görmeyin: istenen eylemin ne yaptığını, hangi dizinleri
ve sistemleri etkilediğini inceleyin. \[4\] \[6\]

## İzin modları

Auto modda ayrı bir sınıflandırıcı model eylemleri çalıştırılmadan önce
inceler. Bu, onay istemlerini azaltır ancak güvenlik garantisi vermez;
hassas işlemlerde insan incelemesinin yerini tutmaz. Sohbette
söylediğiniz "push yapma" gibi sınırlar dikkate alınır, fakat kalıcı
kural değildir ve bağlam sıkıştırıldığında kaybolabilir; kesin garanti
için deny kuralı ekleyin. Deny kuralları bypassPermissions dahil her
modda geçerlidir. \[4\] \[5\]

## Temel güvenlik ilkeleri

Yeni veya güvenilmeyen depolarda önce okuma ve planlamayla başlayın.

Komut izinlerini dar tutun: bilinen, zararsız ve tekrarlanan komutları
(ör. npm test) allowlist'e alın; geniş kabuk veya tüm dosya sistemi izni
vermeyin.

İşletim sistemi seviyesinde sandbox kullanın. İzin kuralları ve sandbox
farklı katmanlardır; birlikte kullanıldıklarında savunma güçlenir. \[6\]

Sırları, API anahtarlarını, üretim kimlik bilgilerini ve müşteri
verilerini prompt'a, loga veya test verisine koymayın. Claude'a değeri
değil, değişken adını ve kullanım kuralını verin.

Web sayfası, issue, log ve MCP'den gelen metni güvenilmeyen girdi sayın;
bu içerik Claude'un kurallarını değiştirmeye çalışan ifadeler
barındırabilir.

İzinleri, kritik dosya değişikliklerini ve bağlı MCP sunucularını
düzenli gözden geçirin; mevcut durumu /permissions ile kontrol edin.

## İnsan onayı gerektiren işler

Üretim veritabanı migration'ı ve şema değişiklikleri, dağıtım, altyapı
ve üretim yapılandırması değişiklikleri, ödeme, kimlik doğrulama ve
yetkilendirme mantığı, toplu veri güncelleme veya silme, dış sistemlere
veri gönderme ve hukuki ya da regülasyon etkisi olan işlerde "yalnızca
planla" veya "uygula ama her adımda onay iste" yaklaşımını kullanın.
Hedef ortamı ve komutları kendiniz doğrulayın; ajan "hazır" dedi diye
onaylamayın.

# 8. Bağlam ve maliyet yönetimi

Bağlam penceresi sohbeti, okunan dosyaları ve komut çıktılarını birlikte
taşır; hızla dolar ve doldukça performans düşer. Gereksiz büyük loglar,
ilgisiz dosyalar ve eski görev konuşmaları hem kaliteyi hem verimliliği
düşürür. \[1\] \[7\]

Bir oturumda tek iş akışı tutun ve oturumlara anlamlı adlar verin (ör.
oauth-migration, billing-race-condition).

Önce ilgili dosya ve testleri okutun; tüm depoyu veya tüm test süitini
gerekmeden yükletmeyin.

Keşif işini alt ajana verin; ana oturuma dosya yolları, kısa akış özeti
ve açık sorular dönsün. \[8\]

Büyük çıktıları dosyaya yönlendirin ve Claude'dan yalnızca ilgili hata
bölümlerini incelemesini isteyin.

/usage içindeki dolar tutarı yerel bir tahmindir ve faturanızdan farklı
olabilir. Abonelik planlarında plan kullanım göstergelerine bakın; API
kullanımında kesin tutar için Console'daki kullanım sayfasını esas alın.
\[7\]

Model seçimini işe göre yapın: rutin kodlama ve test döngülerinde daha
verimli, karmaşık mimari ve derin muhakemede daha güçlü modeli kullanın.
Model adları ve fiyatlar değişebildiğinden güncel seçenekleri /model ve
resmî fiyat sayfasından doğrulayın.

# 9. Takımda ölçeklendirme

Önce küçük bir pilot grupla başlayın; gerçek darboğazları ve bir maliyet
tabanını ölçtükten sonra yaygınlaştırın. Kademeli bir kurulum sırası:
\[12\]

Ortak komutları ve mimari notları sürüm kontrollü CLAUDE.md'de tutun.

Büyük depolarda dizin başına yerel kurallar ve test komutları kullanın;
bu yaklaşım her oturumda bütün kod tabanını anlatmaktan daha iyi
ölçeklenir. \[12\]

Tekrarlanan prosedürleri skill'e, kesin kalite ve politika kapılarını
hook'a taşıyın.

Güvenilir MCP bağlantılarını ve işe yaradığı kanıtlanmış plugin'leri
sonra dağıtın.

Kurum çapındaki kısıtları (yasak komutlar, sandbox, izin modları)
managed settings ile merkezî yönetin.

Otomasyona düşük riskli işlerle başlayın: dokümantasyon kontrolü, test
raporu özeti, statik analiz ve PR incelemesi. Kod değiştiren veya üretim
kaynaklarına erişen otomasyonlarda en az ayrıcalık ilkesini uygulayın.
LSP tabanlı kod gezinme, özellikle tipli ve büyük projelerde sembol
çözümlemesini iyileştirebilir. \[12\]

Yapılandırmayı kalıcı ve dokunulmaz saymayın. Modeller ve Claude Code
yetenekleri değiştikçe eski talimatlar gereksiz veya kısıtlayıcı hâle
gelebilir; ekip ayarlarını düzenli olarak ve büyük model ya da iş akışı
değişikliklerinden sonra gözden geçirin.

# 10. Sık yapılan hatalar

# Hızlı başlangıç kontrol listesi

İlgili dalı açın; git status --short ile çalışma alanını kontrol edin.

claude ile başlayın; ilk kurulumda /doctor ve /init kullanın.

Hassas işte oturumu Manual modda başlatın: claude --permission-mode
default.

/memory ile proje talimatlarının yüklendiğini doğrulayın.

İsteğe hedef, kapsam, sınır, referans ve doğrulama ölçütünü yazın.

Küçük işi doğrudan, belirsiz veya çok dosyalı işi planla başlatın.

İşi küçük parçalara bölün; her parçadan sonra ilgili testleri
çalıştırın.

Diff'i ve test kanıtlarını inceleyin; kritik değişikliklerde bağımsız
inceleme yaptırın.

Küçük, açıklayıcı commit'ler oluşturun; ana dala doğrudan push yapmayın.

İlgisiz göreve geçerken /clear kullanın; tekrarlanan öğrenimleri
CLAUDE.md, kural, skill veya hook'a aktarın.

# Sonuç

Claude Code ile profesyonel verim; planlı çalışma, kalıcı proje bağlamı,
ölçülebilir doğrulama, bağımsız inceleme ve kontrollü otomasyonun
birleşiminden gelir. Hız için kontrolü feda etmeyin: küçük kapsam, net
kabul kriterleri, test kanıtı ve en az ayrıcalıklı erişim,
sürdürülebilir kalitenin temel ilkeleridir.

# Ek A --- Kopyala-yapıştır görev şablonu

Büyük veya kritik görevler için tüm unsurları tek seferde tanımlayan
genel şablon:

# Kaynaklar

Metin içindeki köşeli parantezli numaralar aşağıdaki kaynaklara
bağlantıdır. Erişim tarihi: 28 Eylül 2026.

\[1\] Best practices for Claude Code ---
https://code.claude.com/docs/en/best-practices

\[2\] Common workflows ---
https://code.claude.com/docs/en/common-workflows

\[3\] How Claude remembers your project (CLAUDE.md ve bellek) ---
https://code.claude.com/docs/en/memory

\[4\] Configure permissions ---
https://code.claude.com/docs/en/permissions

\[5\] Choose a permission mode ---
https://code.claude.com/docs/en/permission-modes

\[6\] Security --- https://code.claude.com/docs/en/security

\[7\] Manage costs effectively --- https://code.claude.com/docs/en/costs

\[8\] Subagents --- https://code.claude.com/docs/en/sub-agents

\[9\] Skills --- https://code.claude.com/docs/en/skills

\[10\] Hooks --- https://code.claude.com/docs/en/hooks

\[11\] Model Context Protocol (MCP) ---
https://code.claude.com/docs/en/mcp

\[12\] How Claude Code works in large codebases ---
https://claude.com/blog/how-claude-code-works-in-large-codebases-best-practices-and-where-to-start

  1   Hedefi, kapsamı ve başarı ölçütünü açık yazın.
  --- ------------------------------------------------

  -----------------------------------------------------------------------
  2                                   Belirsiz veya riskli işte önce
                                      keşif ve plan; küçük işte doğrudan
                                      uygulama.
  ----------------------------------- -----------------------------------

  -----------------------------------------------------------------------

  3   "Bitti" değil kanıt isteyin: test, lint, build, ekran görüntüsü.
  --- ------------------------------------------------------------------

  -----------------------------------------------------------------------
  4                                   Bağlamı temiz tutun: kısa
                                      CLAUDE.md, ilgisiz işte /clear,
                                      ağır keşifte alt ajan.
  ----------------------------------- -----------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  5                                   En az yetki: dar izinler, sandbox
                                      ve yüksek etkili işlerde insan
                                      onayı.
  ----------------------------------- -----------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
                                      Komutlar, modlar ve varsayılanlar
                                      sık güncellenir; kritik ayarları
                                      kendi sürümünüzde /doctor,
                                      /permissions ve güncel
                                      dokümantasyonla doğrulayın.
  ----------------------------------- -----------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Unsur                   Netleştirdiği soru      Örnek
  ----------------------- ----------------------- -----------------------
  Hedef                   Kullanıcı veya sistem   Oturum süresi dolan
                          açısından ne değişmeli? kullanıcı yeniden giriş
                                                  yapabilmeli.

  Kapsam ve bağlam        Hangi dosya, modül,     @src/auth/session.ts,
                          hata mesajı veya        tam hata çıktısı,
                          senaryo ilgili?         yeniden üretme adımları

  Sınırlar                Ne korunmalı, ne kapsam Mevcut oturum
                          dışı, neden             davranışını değiştirme;
                          kaçınılmalı?            yeni bağımlılık ekleme.

  Referans                Kod tabanında hangi     Benzer akış için
                          mevcut desen örnek      src/auth/refresh.ts
                          alınmalı?               

  Doğrulama               Başarının gözlenebilir  İlgili testler, lint,
                          kanıtı ne olacak?       tür kontrolü, uçtan uca
                                                  akış
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Oturum süresi dolduktan sonra kullanıcı yeniden giriş yapamıyor. /
  src/auth/ içindeki token yenileme akışını incele. Önce sorunu yeniden
  üreten bir test ekle, ardından kök nedeni düzelt. Mevcut oturum
  davranışını değiştirme. İlgili testleri ve tür kontrolünü çalıştır;
  komutları ve sonuçları raporla.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -------------------------------------------------------------------------------------
  01 Keşfet    02 Planla     03 Uygula    04 Doğrula  05 İncele        06 Kaydet
  ------------ ------------- ------------ ----------- ---------------- ----------------
  Kod tabanını Dosyaları,    Onaylı planı Test, lint, Diff'i bağımsız  Anlamlı commit,
  ve mevcut    riskleri ve   küçük, geri  tür         bir oturumda     PR açıklaması ve
  davranışı    test          alınabilir   kontrolü    değerlendirin.   gerekli
  inceletin.   yaklaşımını   adımlarla    veya build                   dokümantasyon.
               belirletin.   uygulatın.   kanıtı                       
                                          isteyin.                     

  -------------------------------------------------------------------------------------

  -----------------------------------------------------------------------
  İş türü                 Önerilen yaklaşım       Neden
  ----------------------- ----------------------- -----------------------
  Küçük ve açık iş        Doğrudan uygulama ve    Planlama yükü kazançtan
                          hızlı kontrol (yazım    fazladır
                          düzeltmesi, tek         
                          satırlık hata mesajı,   
                          sınırlı log             
                          değişikliği)            

  Hata ayıklama           Önce hatayı yeniden     Semptom değil neden
                          üreten test, sonra kök  hedeflenir
                          neden düzeltmesi        

  Belirsiz veya çok       Keşif → plan modu →     Mimari ve etki alanı
  dosyalı özellik         plan incelemesi →       önceden netleşir
                          uygulama                

  Yüksek riskli alan      Ayrı keşif ve plan,     Hata maliyeti yüksektir
                          test ve geri alma       
                          stratejisi, küçük       
                          commit'ler, bağımsız    
                          inceleme (ör. kimlik    
                          doğrulama, ödeme, veri  
                          silme; tam liste için   
                          bkz. Bölüm 7, İnsan     
                          onayı gerektiren işler) 

  Büyük refaktör          Pilot uygulama, test,   Yanlış yaklaşımın
                          kademeli yayılım        yayılması önlenir

  Keşif ağırlıklı iş      Alt ajana devret; ana   Ana oturumun bağlamı
                          oturuma yalnızca özet,  temiz kalır
                          dosya yolları ve kanıt  
                          dönsün                  
  -----------------------------------------------------------------------

  claude --permission-mode plan
  -------------------------------

  -----------------------------------------------------------------------
                                      Pratik ölçüt: Yapılacak değişikliği
                                      tek cümlede tarif edebiliyorsanız
                                      planı atlayın. Yaklaşım belirsizse,
                                      değişiklik birden çok dosyaya
                                      yayılıyorsa veya alan sizin için
                                      yeniyse planla başlayın.
  ----------------------------------- -----------------------------------

  -----------------------------------------------------------------------

  git status --short
  --------------------

  claude --worktree auth-fix
  ----------------------------

  -----------------------------------------------------------------------
  Hata: \[tam hata metni\]. Şu adımlarla yeniden oluşuyor: \[adımlar\]. /
  / Önce ilgili kod yolunu ve mevcut testleri incele. Sorunu yeniden
  üreten bir test yaz; kök nedeni düzelt, semptomu gizleme veya geçici
  çözüm kullanma. Kapsamı \[dosya/alan\] ile sınırla ve mevcut hata
  yanıtı biçimini koru. / / İlgili testleri, lint'i ve tür kontrolünü
  çalıştır. Sonunda değişen dosyaları, gerekçelerini, komutları ve
  sonuçlarını özetle.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  \[Özellik\] için beklenen kullanıcı davranışı: \[davranış\]. Henüz kod
  yazma. / / Önce benzer uygulamaları bul ve mevcut mimariyi özetle.
  Ardından şunları içeren bir plan hazırla: / - Değişecek dosyalar ve
  gerekçeleri / - Yeniden kullanılacak mevcut desenler / - API, veri
  modeli ve yetkilendirme etkileri / - Kenar durumlar ve riskler / - Test
  stratejisi ve kapsam dışı konular / / Belirsiz ürün kararlarını ayrıca
  soru olarak listele. Plan onaylandıktan sonra uygula, testleri çalıştır
  ve kanıtları paylaş.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  \[Alan/dosya\] bölümünü \[hedef desen\] doğrultusunda refaktör et.
  Dışarıdan gözlenen davranış ve API uyumluluğu korunsun. / / Önce mevcut
  testleri ve kullanım noktalarını bul. Her küçük adımdan sonra test et;
  yeni bağımlılık ekleme. Sonunda diff'i ve tüm doğrulama sonuçlarını
  raporla.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Bu depoda \[alan/akış\] nasıl çalışıyor? Önce ilgili giriş noktalarını
  bul, ardından çağrı akışını ve temel veri yapılarını dosya yollarıyla
  açıkla. / Mevcut testlerin bu davranışı nasıl doğruladığını da belirt.
  Kod değiştirme.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Bir alt ajan kullanarak kimlik doğrulama sistemimizi incele. Şunları
  raporla: / - Token yenileme akışı ve OAuth ile ilgili mevcut
  yardımcılar / - Oturum saklama modeli / - Yetkilendirme kontrollerinin
  bulunduğu katmanlar / - Yeniden kullanılabilir dosya ve fonksiyonlar /
  / Kod değiştirme. Yalnızca ilgili dosya yollarını, bulguları ve
  riskleri özetle.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Mevcut diff'i \[PLAN.md / issue\] ile karşılaştırarak bağımsız bir kod
  incelemesi yap. Kod değiştirme. / / Yalnızca somut bulguları, önem
  sırasına göre ve dosya/satır referansıyla raporla: / - Gereksinim
  eksikleri ve mantık hataları / - Geriye dönük uyumsuzluk / - Güvenlik,
  yetkilendirme veya veri sızıntısı riski / - Eşzamanlılık ve yarış
  koşulları / - Eksik veya yanlış testler; görev kapsamı dışına çıkan
  değişiklikler / / Bulgu yoksa bunu ve hangi kontrolleri yaptığını
  belirt. Spekülatif stil önerisi verme.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  İşi tamamlamadan önce: / 1. Değişiklik için ilgili testleri çalıştır. /
  2. Lint, tür kontrolü ve gerekiyorsa build çalıştır. / 3. Başarısız
  kontrolleri kök nedeni düzelterek yeniden çalıştır. / 4. Şu biçimde
  rapor ver: değişen dosyalar, davranış değişikliği, çalıştırılan
  komutlar ve sonuçları, bilinen sınırlamalar ve riskler, manuel kontrol
  gereken noktalar.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Girmeli                             Girmemeli
  ----------------------------------- -----------------------------------
  Claude'un tahmin edemeyeceği        Claude'un koddan zaten
  komutlar (test, tek test, lint,     çıkarabileceği bilgiler
  build)                              

  Varsayılandan farklı kod stili      Dilin standart konvansiyonları
  kuralları                           

  Projeye özgü mimari kurallar ve     "Temiz kod yaz" gibi genel
  kritik tuzaklar                     tavsiyeler

  Git, test ve teslim kuralları       Yalnızca bazı işlerde gereken
                                      ayrıntılı prosedürler (→ skill)
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  \# Proje / B2B sipariş yönetim API'si (TypeScript, Node.js). / / \#
  Komutlar / - Kurulum: npm ci / - Birim testleri: npm test / - Tek test:
  npm test -- `<dosya>`{=html} / - Lint: npm run lint / - Tür kontrolü:
  npm run typecheck / - Build: npm run build / / \# Kod standartları / -
  TypeScript strict mode zorunlu. / - Yeni API endpoint'lerini
  src/api/routes altında oluştur. / - Public API değişikliklerinde
  OpenAPI dokümantasyonunu güncelle. / - Yeni bağımlılık eklemeden önce
  gerekçeyi açıkla ve onay iste. / / \# Test / - Davranış değişikliği
  için test ekle veya mevcut testi güncelle. / - İlgili testleri
  çalıştırmadan görevi tamamlandı sayma. / - Harici servis testlerinde
  gerçek kimlik bilgisi kullanma. / / \# Git / - main dalına doğrudan
  commit veya push yapma. / - Commit mesajları Conventional Commits
  biçiminde olsun. / / \# Alan notları / - Faturalama kuralları:
  src/billing/CLAUDE.md
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Araç                    Ne zaman                Örnek
  ----------------------- ----------------------- -----------------------
  CLAUDE.md               Bilgi her oturumda      Komutlar, mimari
                          gerekli                 kurallar, Git kuralları

  Yol kapsamlı kural      Kural yalnızca belirli  .claude/rules/ altında
                          dizin veya dosya        faturalama kuralları
                          türünde geçerli         

  Skill                   Prosedür ara sıra       Sürüm kontrol listesi,
                          gerekiyor; içerik       güvenlik incelemesi,
                          yalnızca ilgili         "issue al → düzelt →
                          olduğunda yüklenir      test et → PR hazırla"

  Hook                    Eylem her koşulda       Dosya değişince
                          otomatik ve             biçimlendirme, belirli
                          deterministik çalışmalı dizine yazmayı
                                                  engelleme

  Alt ajan                Yan görev ana oturumun  Büyük keşif, mimari
                          bağlamını dolduracak    veya güvenlik
                                                  incelemesi, bağımsız
                                                  doğrulama

  MCP                     Harici sisteme doğrudan Issue takip sistemi,
                          erişim                  dokümantasyon,
                          kopyala-yapıştırı       veritabanı
                          azaltıyor               

  Plugin                  Ekipte kanıtlanmış      Skill, hook ve MCP
                          yapılandırmaları        ayarlarının ekip paketi
                          birlikte dağıtmak       

  Managed settings        Kurum çapında zorunlu   Yasak komutlar, sandbox
                          politika                politikası, izin modu
                                                  kısıtları
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Mod                     Sormadan çalışanlar     Uygun olduğu durum
  ----------------------- ----------------------- -----------------------
  default (Manual)        Yalnızca okuma          Her eylemi kendiniz
                                                  onaylamak; hassas
                                                  işler, tanımadığınız
                                                  kod

  acceptEdits             Okuma, dosya düzenleme  İncelediğiniz kod
                          ve yaygın dosya sistemi üzerinde hızlı yineleme
                          komutları               

  plan                    Okuma (auto mod         Değiştirmeden önce
                          mevcutsa                keşif ve planlama
                          sınıflandırıcının       
                          onayladığı komutlar)    

  auto                    Her şey; arka planda    Genel yönüne
                          güvenlik denetimiyle    güvendiğiniz uzun
                                                  görevler

  dontAsk                 Okuma ve önceden onaylı Kilitli CI ortamları ve
                          araçlar; gerisi         betikler
                          reddedilir              

  bypassPermissions       Her şey                 Yalnızca izole
                                                  konteyner ve VM'ler
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
                                      Önemli: varsayılan mod değişti.
                                      Güncel sürümlerde Pro, Max ve Team
                                      planlarında yerleşik başlangıç modu
                                      auto'dur. Hassas bir projede her
                                      eylemi kendiniz onaylamak
                                      istiyorsanız oturumu açıkça Manual
                                      modda başlatın: claude
                                      --permission-mode default. Kalıcı
                                      yapmak için
                                      \~/.claude/settings.json içinde
                                      permissions.defaultMode değerini
                                      "default" olarak ayarlayın. \[5\]
  ----------------------------------- -----------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
                                      Pratik başlangıç: Yeni başlayanlar
                                      için Manual mod ve proje içinde
                                      sınırlı erişim iyi bir öğrenme
                                      düzenidir. Sandbox ve dar izinler
                                      oturduktan sonra düşük riskli,
                                      tekrar eden işlerde acceptEdits
                                      veya auto moda geçerek otomasyonu
                                      artırın; yüksek etkili işlerde
                                      insan incelemesini koruyun.
  ----------------------------------- -----------------------------------

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Komut                               Ne zaman kullanılır
  ----------------------------------- -----------------------------------
  /clear                              İlgisiz yeni bir göreve geçerken
                                      temiz bağlam açmak için

  /compact                            Uzun bir görevde önemli kararları
                                      ve test bilgisini koruyarak bağlamı
                                      özetlemek için

  /context                            Bağlamda neyin ne kadar yer
                                      kapladığını görmek için

  /memory                             Hangi CLAUDE.md ve kural
                                      dosyalarının yüklendiğini kontrol
                                      etmek için

  /usage                              Token kullanımını ve plan
                                      limitlerini izlemek için

  /rewind                             Riskli bir denemeden sonra önceki
                                      bir kontrol noktasına dönmek için

  /model                              İşe uygun modeli seçmek için
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Hata                                Doğrusu
  ----------------------------------- -----------------------------------
  "Uygula" deyip kabul ölçütü         Beklenen davranışı ve
  vermemek                            çalıştırılacak testleri isteğe
                                      ekleyin.

  İlk adımda her dosyayı okutmak      Önce kapsamı daraltın; dosyaları
                                      görev ilerledikçe açtırın.

  Küçük işlere planlama yükü eklemek  Planı belirsizlik, risk veya çok
                                      dosyalı değişiklik için kullanın.

  Büyük ve belirsiz işi tek prompt'ta Önce keşif ve taslak, sonra küçük
  istemek                             uygulama adımları.

  Test çalıştırmadan "tamam" saymak   Başarının gözlenebilir kanıtını
                                      isteyin.

  Aynı oturuma ilgisiz işler yığmak   /clear ile temiz bağlam açın.

  CLAUDE.md'yi ansiklopediye çevirmek Yalnızca her oturumda işe yarayan
                                      bilgiyi bırakın; gerisini kurala
                                      veya skill'e taşıyın.

  Her eyleme geniş ve kalıcı izin     En az yetki ilkesini uygulayın ve
  vermek                              sandbox kullanın.

  Varsayılan modu bilmeden hassas işe Hassas işte oturumu açıkça Manual
  başlamak                            modda başlatın (bkz. Bölüm 7, İzin
                                      modları).

  Kodu yazan oturumu tek inceleyici   Kritik değişikliklerde bağımsız
  saymak                              inceleme veya ayrı doğrulama
                                      kullanın.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Rol: Bu depoda kıdemli bir yazılım mühendisi olarak çalış. / / Hedef:
  \[İstenen davranış değişikliğini açıkça yaz\] / / Kapsam: / -
  İncelenecek alanlar: \[dosya/klasör/modül\] / - Referans alınacak
  mevcut örnek: \[dosya veya bileşen\] / - Kapsam dışı: \[dokunulmaması
  gereken alanlar\] / / Kısıtlar: / - Mevcut mimari ve kod standartlarına
  uy. / - Yeni bağımlılık eklemeden önce gerekçeyi ve alternatifleri
  açıkla. / - Güvenlik, yetkilendirme ve hata yönetimi standartlarını
  koru. / - Geriye uyumluluğu bozacak değişiklikleri önceden belirt. / /
  Çalışma biçimi: / 1. Önce kodu incele. / 2. Kod yazmadan önce değişecek
  dosyaları, yaklaşımı ve riskleri içeren bir plan sun. / 3. Plan
  onaylandıktan sonra uygula. / 4. Davranış değişikliğini kanıtlayan
  testleri ekle veya güncelle. / 5. İlgili testleri, lint'i, tür
  kontrolünü ve gerekiyorsa build'i çalıştır. / 6. Başarısız sonuçları
  kök nedeni düzelterek yeniden çalıştır. / 7. Son diff için bağımsız bir
  inceleme yap. / / Teslim biçimi: özet; değişen dosyalar ve gerekçeleri;
  test ve komut sonuçları; riskler ve manuel kontrol noktaları; takip işi
  önerileri.
  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
