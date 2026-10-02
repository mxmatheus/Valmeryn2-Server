# Valmeryn2 Server

Valmeryn2 sunucusunun çalışma dosyaları, locale/quest içerikleri, proto kaynakları ve yönetim yardımcı betikleri.

## Bileşenler

- `share/`: oyun verisi, locale, quest, proto ve sunucu yapılandırmaları.
- `sql/`: proje veritabanı SQL kaynakları ve şema güncellemeleri.
- `start.py`, `channels.py`, `stop.py`: sunucu başlatma/durdurma yardımcıları.

İlgili kaynak: `Valmeryn2-Server-Src`.

## Kurulum ilkeleri

1. Önce server source'u derleyin ve aynı revizyondaki `game`/`db` çıktılarıyla çalışma dosyalarını hazırlayın.
2. Test için yeni ve ayrı bir MariaDB/MySQL instance'ı ile boş proje şemaları kullanın. Önceki devir planında yeni DB için 3309 önerilmiştir; eski kurulumun 3308 portuna veya şemalarına bağlanmayın.
3. `share/conf` bağlantı ayarlarını yerel ortamınıza göre düzenleyin ve parolaları Git'e eklemeyin.
4. SQL kurulumlarını yalnızca yeni boş şemalarda yedek ve doğrulama alarak uygulayın.
5. Önce auth, DB, channel ve client bağlantısını ayrı ayrı kontrol edin.

Bu çalışma ortamında şu anda yeni Valmeryn DB örneği veya oyun server süreci doğrulanmış değildir. `mxmatheus` test hesabı ve karakteri yalnızca yeni DB kurulduktan sonra oluşturulmalıdır.

## Sistem durumu

Çalışma alanındaki `YENI_PROJE_DEVIR_RAPORU.md` önceki sistem kataloğunu ve açık oyun içi doğrulama maddelerini içerir. Bu repository temiz M2Dev ana dalından başlıyor; rapordaki özellikleri mevcut sunucuya entegre edilmiş kabul etmeyin. Migration ve runtime eşleşmesi olmadan canlı/önceki veritabanında değişiklik yapmayın.
