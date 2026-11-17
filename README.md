# Neden bu mimari?

# Monolit uygulama. Mikroservis kurma. Tek bir API (Python/FastAPI öneririm, WebSocket desteği hazır), PostgreSQL ve Redis yeterli. Hedefin sistem/altyapı rolleri olduğu için uygulama kodu basit kalsın, projenin yıldızı altyapı olsun.

# Özellikler. Kayıt/giriş, sunucu/kanal yapısı, gerçek zamanlı mesajlaşma ve mesaj geçmişi. Sesli sohbet (WebRTC) kapsam dışı, onu bırak.

# Önce yerel, sonra AWS. Her şeyi önce docker-compose ile kendi bilgisayarında (ya da VirtualBox’taki bir Ubuntu Server VM’de) çalıştır, sonra aynısını AWS’ye taşı. Böylece uygulama hatası ile altyapı hatasını birbirine karıştırmazsın.

# Önce EC2, sonra ECS. Docker’ı EC2'de kendin çalıştırman Linux’u pratikte öğretir. ECS/Fargate’e geçiş istersen en sonda isteğe bağlı bir faz olur.

# Private erişim. Sadece WireGuard sunucusunun UDP portu dışarı açık, uygulama ve veritabanı private subnette. SSH’ı kapatıp SSM Session Manager ile bağlanırsın. Bu bölümü zaten izleyeceksin, ve CV’de iyi görünen bir güvenlik detayı olur.

# Yol haritası

# 

# Süreler, günde 1-2 saat çalışıp CCNA’yı paralel sürdürdüğün varsayımıyla tahmini:

# 

# Faz	Süre	İçerik

# 0	2-4 gün	Kalan AWS bölümlerini bitir. CloudFormation (IaC fikri), SSM Session Manager ve Cost Explorer projede doğrudan lazım. GitHub’da repo aç, README’ye hedef mimariyi koy.

# 1	1-1,5 hafta	3 saatlik Docker videosu + Linux temelleri. Her Docker bölümünde videodaki örneği bırakıp kendi projenin parçasını konteynerleştir.

# 2	2-3 hafta	Yerel MVP: Nginx + API + PostgreSQL + Redis, docker-compose ile. Sırrı (şifre, anahtar) koda gömme, .env kullan, .gitignore’a ekle.

# 3	1-2 hafta	AWS’ye elle kurulum (konsoldan): VPC, subnetler, route table, security group, EC2, RDS, S3, IAM role.

# 4	1 hafta	WireGuard VPN. Security group’ta sadece VPN portu açık, uygulamaya sadece VPN üzerinden erişim.

# 5	1-2 hafta	Aynı altyapıyı Terraform ile koda dök. terraform destroy ile silip yeniden kurabildiğinde faz tamam.

# 6	1 hafta	GitHub Actions ile otomatik deploy, CloudWatch alarmı, Budget alarmı, README + mimari şeması + CV maddesi.

# 

# Toplamda 2,5-3 ay civarı. İsteğe bağlı faz 7: projeyi herkese açmak (ALB, ACM sertifikası, Route 53).

# 

# Öğrendiklerinle bağlantı

# CCNA: Subnetting/CIDR (VPC IP planı), NAT, ACL ve route table doğrudan kullanılacak. STP projede gerekmiyor, istersen o videoya kadar ara vermeden devam et.

# AWS: VPC, EC2, RDS, S3, IAM, CloudWatch, CloudFormation ve SSM hepsi diyagramda yer alıyor.

# Linux ve Docker: Projenin içinde, EC2'de gerçek bir sunucu yönetirken öğrenilecek.

# Dikkat edilecekler

# Maliyet: NAT Gateway, RDS ve ELB saat bazlı ücretlenir ve ücretsiz katmanın dışında kalabilir. Faz 3'e geçmeden önce Budget alarmı kur, çalışmadığın zamanlarda kaynakları kapat veya Terraform’a geçince destroy et. Güncel fiyatları AWS fiyat sayfasından kontrol et. Maliyeti düşürmenin bir yolu, private subnet’in internet erişimi için ayrı bir NAT Gateway yerine WireGuard EC2'sini aynı zamanda NAT olarak kullanmak, ama bunu ilk kurulumda değil, çalışan bir yapı oluştuktan sonra dene.

# Kapsamı küçük tut: Önce “iki kişi bir kanalda yazışıyor” seviyesine ulaş, sonra özellik ekle.

# Git disiplini: Küçük ve açıklayıcı commit’ler at. İşverenler çoğu zaman kodu değil commit geçmişini ve README’yi inceler.

# Öğrenme kaynakları (video ve interaktif lab ağırlıklı)

# Linux: OverTheWire Bandit (tarayıcı/SSH ile oyunlaştırılmış lab) ve Linux Journey (interaktif ders). İkisi de ücretsiz.

# Docker: Planladığın 3 saatlik video, ardından Play with Docker gibi tarayıcıda çalışan ortamlarla pratik.

