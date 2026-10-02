# Valmeryn2 Server

Valmeryn2 sunucusunun çalışma dosyaları, locale/quest içerikleri, proto kaynakları ve yönetim yardımcı betikleri.

## Bileşenler

- `share/`: oyun verisi, locale, quest, proto ve sunucu yapılandırmaları.
- `sql/`: proje veritabanı SQL kaynakları ve şema güncellemeleri.
- `start.py`, `channels.py`, `stop.py`: sunucu başlatma/durdurma yardımcıları.

İlgili kaynak: `Valmeryn2-Server-Src`.

## Kurulum ilkeleri

1. Önce server source'u derleyin ve aynı revizyondaki `game`/`db` çıktılarıyla çalışma dosyalarını hazırlayın.
2. Yeni proje veritabanı için ayrı instance/data dizini ve MySQL portu `3309` kullanın; eski kurulumun 3308 portuna veya şemalarına bağlanmayın.
3. `share/conf` bağlantı ayarlarını yerel ortamınıza göre düzenleyin ve parolaları Git'e eklemeyin.
4. SQL kurulumlarını yalnızca yeni boş şemalarda yedek ve doğrulama alarak uygulayın.
5. Önce auth, DB, channel ve client bağlantısını ayrı ayrı kontrol edin.

## Yerel geliştirme portları

| Bileşen | Port | Ayar kaynağı |
|---|---:|---|
| Auth | 24000 | `install.py` auth CONFIG üreticisi |
| CH1 ilk core | 24011 | `install.py` channel CONFIG üreticisi |
| CH2 ilk core | 24021 | `install.py` channel CONFIG üreticisi |
| DB game-listener | 9000 | `share/conf/db.txt` içindeki `BIND_PORT` ve `share/conf/game.txt` içindeki `DB_PORT` |
| MySQL | 3309 | `share/conf/db.txt` içindeki `SQL_*` bağlantıları |

MySQL portu auth/channel/game-listener portlarının yerine kullanılmaz. `channels/<ad>/CONFIG` dosyaları `install.py` çalıştırıldığında üretilir; installer mevcut `channels` klasörünü silip yeniden oluşturduğu için yalnızca yeni runtime kurulurken çalıştırın. CH1/CH2 dışındaki core'lar kanal numarasına göre 24000 tabanından devam eder. P2P portları ayrı olarak 12000 tabanını kullanır.

SQL dump'larında MariaDB'ye özgü `ENGINE=Aria` tablolar bulunur. Bunları MySQL 5.6'ya değiştirmeden aktarmayın; hedef veritabanı motoruna göre şema uyumluluğunu belirleyip migration'ları doğrulayın.

Yeni oyun tablolarını aktarmadan önce dump ve hedef motor uyumluluğunu doğrulayın. Bu depodaki SQL dump'ları `ENGINE=Aria` içerdiği için doğrudan MySQL 5.6'ya yüklenemez. `mxmatheus` test hesabı ve karakteri, uyumlu şemalar yeni instance'a aktarıldıktan sonra oluşturulmalıdır.

## Sistem durumu

Çalışma alanındaki `YENI_PROJE_DEVIR_RAPORU.md` önceki sistem kataloğunu ve açık oyun içi doğrulama maddelerini içerir. Bu repository temiz M2Dev ana dalından başlıyor; rapordaki özellikleri mevcut sunucuya entegre edilmiş kabul etmeyin. Migration ve runtime eşleşmesi olmadan canlı/önceki veritabanında değişiklik yapmayın.
