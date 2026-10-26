# ShopTest – Test Planı ve Gereksinim Analizi

*Test edilen sistem: SauceDemo (https://www.saucedemo.com) | Sürüm: 1.0 | Hazırlayan: QA Adayı*

## 1. Giriş ve Amaç

Bu doküman, SauceDemo e-ticaret demo uygulamasının manuel ve otomasyon testlerinin kapsamını, yaklaşımını, ortamını ve teslim edilecek çıktılarını tanımlar. Amaç, uçtan uca bir QA süreci uygulayarak portföye girecek profesyonel bir proje üretmektir.

## 2. Kapsam

### Kapsam dahilinde
- Giriş (Login) ve oturum kapatma
- Ürün listeleme ve sıralama
- Ürün detay sayfası
- Sepet işlemleri (ekleme, çıkarma)
- Ödeme akışı (Checkout: bilgi, özet, tamamlama)
- Yan menü (All Items, About, Logout, Reset App State)
- Temel API testleri (Petstore / Reqres üzerinden)

### Kapsam dışı
- Gerçek ödeme entegrasyonu
- Yük ve stres testleri (ileri aşamada ayrıca değerlendirilebilir)
- Mobil yerel uygulama testleri

## 3. Test Edilecek Gereksinimler

| ID | Modül | Gereksinim | Öncelik |
|---|---|---|---|
| REQ-01 | Login | Geçerli kullanıcı adı ve şifre ile giriş yapılabilmelidir | Yüksek |
| REQ-02 | Login | Hatalı veya boş bilgilerle giriş engellenmeli ve anlamlı hata mesajı gösterilmelidir | Yüksek |
| REQ-03 | Login | Kilitli kullanıcı (locked_out_user) giriş yapamamalıdır | Orta |
| REQ-04 | Ürünler | Ürün listesi 6 ürünü ad, açıklama, fiyat ve görselle göstermelidir | Yüksek |
| REQ-05 | Ürünler | Sıralama (A-Z, Z-A, fiyat artan, fiyat azalan) doğru çalışmalıdır | Orta |
| REQ-06 | Ürün Detay | Ürüne tıklanınca doğru detay sayfası açılmalıdır | Orta |
| REQ-07 | Sepet | Ürün sepete eklenebilmeli, sepet rozeti doğru sayıyı göstermelidir | Yüksek |
| REQ-08 | Sepet | Sepetten ürün çıkarılabilmelidir | Yüksek |
| REQ-09 | Sepet | Sepet, sayfa geçişlerinde içeriğini korumalıdır | Orta |
| REQ-10 | Checkout | Ad, soyad ve posta kodu zorunlu alanlar olarak doğrulanmalıdır | Yüksek |
| REQ-11 | Checkout | Özet ekranı ürün toplamını, vergiyi ve genel toplamı doğru hesaplamalıdır | Yüksek |
| REQ-12 | Checkout | Sipariş tamamlandığında onay mesajı gösterilmelidir | Yüksek |
| REQ-13 | Menü | Logout işlemi oturumu sonlandırıp login sayfasına yönlendirmelidir | Yüksek |
| REQ-14 | Menü | Reset App State sepeti sıfırlamalıdır | Düşük |
| REQ-15 | Güvenlik | Login olmadan doğrudan URL ile ürün sayfasına erişilememelidir | Yüksek |

## 4. Test Verisi (Hazır Kullanıcılar)

| Kullanıcı | Şifre | Amaç |
|---|---|---|
| standard_user | secret_sauce | Normal akış |
| locked_out_user | secret_sauce | Kilitli hesap senaryosu |
| problem_user | secret_sauce | Hatalı davranış / görsel sorunlar |
| performance_glitch_user | secret_sauce | Yavaş yanıt senaryosu |
| error_user | secret_sauce | Hata üreten akışlar |
| visual_user | secret_sauce | Görsel kusurlar |

## 5. Test Yaklaşımı

- **Manuel test:** Fonksiyonel, kullanılabilirlik ve uyumluluk testleri; en az 30 test durumu.
- **Otomasyon:** Java + Selenium WebDriver + TestNG, Page Object Model, veri tabanlı testler.
- **API testi:** Postman koleksiyonu ve temel doğrulamalar (durum kodu, yanıt gövdesi).
- **Test türleri:** Smoke, Sanity, Regresyon, Fonksiyonel, Fonksiyonel olmayan (temel).
- **Test teknikleri:** Eşdeğerlik sınıfları, sınır değer analizi, karar tablosu, durum geçişi.

## 6. Test Paketleri

| Paket | İçerik | Ne zaman koşulur |
|---|---|---|
| Smoke | Login, ürün listesi, sepete ekleme, checkout tamamlama (4-5 test) | Her yeni sürümde ilk iş |
| Sanity | Düzeltilen hata ve etkilediği alanın hızlı kontrolü | Hata düzeltmesinden sonra |
| Regresyon | Tüm modüllerin tam senaryo seti | Büyük değişiklik ve sürüm öncesi |

## 7. Test Ortamı ve Araçlar

| Alan | Seçim |
|---|---|
| Tarayıcılar | Chrome (ana), Firefox, Edge |
| İşletim sistemi | Windows / macOS / Linux |
| Dil ve IDE | Java 17+, IntelliJ IDEA veya Eclipse |
| Test framework | TestNG, Maven |
| Hata takibi | Jira |
| Test yönetimi | TestRail / Zephyr veya tablo (Excel / Sheets) |
| API | Postman, Swagger |
| Sürüm kontrol | Git + GitHub |
| CI (bonus) | Jenkins |

## 8. Giriş ve Çıkış Kriterleri

**Giriş kriterleri:** Gereksinimler netleşmiş, test ortamı erişilebilir, test verisi hazır, test planı onaylanmış.

**Çıkış kriterleri:** Tüm planlı test durumları çalıştırılmış, kritik ve yüksek öncelikli hataların tamamı kapatılmış veya kabul edilmiş, test raporu tamamlanmış.

## 9. Hata Yönetimi

**Hata yaşam döngüsü:** Yeni → Atandı → Açık → Düzeltildi → Yeniden Test → Kapatıldı (veya Yeniden Açıldı / Reddedildi / Ertelendi).

**Önem derecesi:** Kritik, Yüksek, Orta, Düşük.

**Bir bug raporunda bulunması gerekenler:** Başlık, ortam, adımlar, beklenen sonuç, gerçekleşen sonuç, önem ve öncelik, ekran görüntüsü.

## 10. Riskler

| Risk | Etki | Önlem |
|---|---|---|
| Demo sitenin bakıma girmesi veya değişmesi | Testler kırılır | Locator'ları tek yerde (POM) tut, sürüm notu al |
| Dinamik elementlerde kararsız (flaky) testler | Güvenilmez sonuç | Explicit wait kullan |
| Zaman yetersizliği | Eksik kapsam | Öncelikli gereksinimlerle başla |

## 11. Teslim Edilecek Çıktılar

1. Test Planı (bu doküman)
2. Test durumları tablosu (30+)
3. Çalıştırma sonuçları ve bug raporları
4. Selenium + TestNG + POM framework'ü
5. Postman API koleksiyonu
6. Test Raporu (özet ve metrikler)
7. README'si hazır GitHub reposu

## 12. Zaman Çizelgesi (Öneri)

| Hafta | Odak |
|---|---|
| 1 | Plan, gereksinimler, test durumları |
| 2 | Manuel test çalıştırma ve bug raporlama |
| 3 | Java + Selenium kurulumu, ilk otomatik testler |
| 4 | TestNG, POM, data-driven testler |
| 5 | API testleri, raporlama, Jenkins |
| 6 | Dokümantasyon, GitHub, CV ve mülakat hazırlığı |
