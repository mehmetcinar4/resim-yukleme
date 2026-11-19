# resim-yukleme

PHP İletişim Formu ve Görsel Galerisi
PHP 8+ ve MySQL/MariaDB ile çalışan, yönetici girişli iletişim formu ve görsel galerisi.
Gereksinimler
PHP 8.0 veya üzeri (`pdo_mysql` eklentisi etkin)
MySQL 5.7+ veya MariaDB
Apache, Nginx ya da PHP'nin yerleşik geliştirme sunucusu
Kurulum
`schema.sql` dosyasını MySQL'de çalıştırın. Bu dosya `contact_form` veritabanını ve tabloları oluşturur:
```sh
   mysql -u root -p < schema.sql
   ```
Mevcut bir kuruluma görsel galerisi ekliyorsanız yeni `images` tablosunu oluşturmak için bu komutu tekrar çalıştırın.
Veritabanı bağlantı bilgilerini ortam değişkenleri olarak ayarlayın. Varsayılanlar yerel geliştirme içindir:
```text
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_NAME=contact_form
   DB_USER=root
   DB_PASS=
   ```
Yönetici hesabını oluşturun. Parolayı komuta yazmak yerine ortam değişkeniyle sağlayın:
```sh
   export ADMIN_PASSWORD='guclu-ve-essiz-bir-parola'
   php bin/create-admin.php yonetici
   unset ADMIN_PASSWORD
   ```
`ADMIN_PASSWORD` en az 12 karakter olmalıdır. Yönetici parolası veritabanında `password_hash()` ile hash'lenerek saklanır.
Proje kökünü web sunucunuzun belge kökü yapın. Geliştirme için:
```sh
   php -S 127.0.0.1:8000
   ```
Form `http://127.0.0.1:8000/`, mesaj yönetimi `http://127.0.0.1:8000/admin/` ve görsel galerisi `http://127.0.0.1:8000/admin/images.php` adresindedir. Galeri yönetici girişi gerektirir; yüklenen görsel bağlantıları paylaşılabilir.
Görseller `uploads/` klasöründe saklanır. Web sunucusunun bu klasörü oluşturma ve yazma izni olmalıdır. JPEG, PNG, GIF ve WebP biçimleri desteklenir; dosya başına sınır 10 MB'dır. PHP ayarlarında `upload_max_filesize` en az `10M`, `post_max_size` ise en az `11M` olmalıdır.
Üretimde HTTPS kullanın; PHP hata gösterimini kapatıp hata günlüklerini etkinleştirin. Proje kökünü herkese açık sunuyorsanız `schema.sql`, `bin/` ve yapılandırma dosyalarına HTTP üzerinden erişimi web sunucusunda engelleyin veya yalnızca `index.php`, `admin/` ve `assets/` dosyalarını belge köküne yayınlayın.
