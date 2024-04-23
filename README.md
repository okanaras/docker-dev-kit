# A. WSL Kurulumu & Kaldirma </br>

## 1- kurulum icin </br>

<b>"wsl --install"</b> koumutunu calistir. </br></br>

## 2- varsayilan distro atama </br>

'wsl --list' ile listele. Eger ki ubuntu default degilse asagidaki kodu calistir</br>
wsl --setdefault DISTRO-NAME -> <b>wsl --setdefault Ubuntu</b></br></br>

## 3- Sırasıyla aşağıdaki komutları girerek Ubuntu güncellemelerimizi ve gerekli paketlerimizi kuralım. </br>

sudo apt update </br>
sudo apt upgrade -y </br>
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates </br>
sudo apt install git </br></br>

## 4- NodeJS kuralumu. </br>

sudo apt-get update </br>
sudo apt-get install -y ca-certificates curl gnupg </br>
sudo mkdir -p /etc/apt/keyrings </br>
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg </br></br>

NODE*MAJOR=20 </br>
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node*$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list </br></br>

sudo apt-get update </br>
sudo apt-get install nodejs -y </br></br>

## 5- Alternative node npm kurulumu</br></br>

(a) sudo apt update -y</br>
(b) sudo apt upgrade -y</br>
(c) sudo apt-get install nodejs -y</br>
(d) sudo apt install npm -y</br></br>

## 6- WSL Kaldirma </br></br>

1- Uygulamalardan ubuntuyu kaldir. </br>
2- terminalde <b>"wsl --list"</b> koumutunu calistir. </br>
3- terminalde <b>"wsl --unregister Ubuntu"</b> koumutunu calistir. </br></br></br></br>

# B. Github Kurulumu </br>

## 1- Asagidaki kodlar git kurulum kodlaridir hepsi ubuntu terminalinde calisacak! </br>

sudo apt install git || git --version </br>
git config --global user.name "Okan Aras" </br>
git config --global user.email "oknaras@icloud.com" </br>
git config --global init.defaultBranch main </br>
cat ~/.gitconfig </br></br>

## 2- SSH kurulumu </br>

ssh-keygen -t rsa -b 4096 -C "okanaras" </br>
cikan ekranda public key yazan bolumdeki /root/.ssh/id_rsa.pub yazan yerde asagidaki komutu yaziyoruz </br></br>
<b>code ~//.ssh/id_rsa.pub</b> </br></br>
komutu ile vscode ta key i aciyoruz ve key i kopyalayip github web te settings-ssh and gpg keys yerine girip yeni ssh ekliyoruz </br></br>
title'a "Ubuntu-WSL" verdim "key tipi auth" ve "key e yukarda kopyaladigimi" verip ekledim </br></br>

ssh -T git@github.com </br>
<b>'yes'</b> diyoruz </br>
en sonda "git clone 'sshlinki'" ile projeyi cekiyoruz </br></br></br></br>

# C. Docker Desktop </br>

## Uygulama ayarlari

Docker Desktop(Windows) indirelim ve kuralım. </br>
Kurulum sonrasında Docker Desktop uygulamamızı açalım ve sağ üstteki ikona tıklayarak ayarlar menüsüne gidelim. </br></br>
General bbölümünde 'Use WSL 2 ve Use Docker Compose V2' seçili olsun. </br></br>
Ardından Resources - WSL Integration kısmında Ubuntu seçeneğini aktif edelim.</br></br>
nginx defaulta ayaga kalkacak path, domain ve php surumunu veriyoruz ve ../etc/hosts a ayni domaini veriyoruz. </br></br>
docker-compose up -d ile ayaga kaldiriyoruz docker ps ile docker daki container lara bakip ilgili container in id sine docker exec -it "id" bash ile baglaniyoruz daha sonra cd ile iligli laravel klasorumuze giriyoruz</br>

docker-compose stop </br>
docker-compose down</br>
docker-compose up -d --build</br>
docker-compose build --no-cache</br></br>

## laravel env de ise

app_url="url", (http://eloquent.com) </br>
db_host=mysql, (yml icinde verilen ad) </br>
db_password="pass" (12345678) </br></br></br></br>

# D. Proje Klonlama & Hata Giderme </br>

## 1- projeyi klonlamak icin once ubuntu dan home/okanaras 'a docker-mysql klonla.</br>

git clone https://github.com/okanaras/docker-mysql.git</br></br>

## 2- Projelerini cekmek icin docker a baglan ve terminale </br>

docker ps -> docker exec -it "id" bash -> git clone https://github.com/okanaras/yazilim_egitim_blog.git </br></br>

## 3- egerki vs code'tayken permission hatasi varsa bu kodu ubuntu terminale yapistir</br>

sudo chown -R okanaras /home/okanaras</br></br>

## 5- The stream or file "/var/www/html/yazilim_egitim_blog/storage/logs/laravel.log" could not be opened in append'</br>

sudo chmod -R 775 storage/</br></br>

## 6- The /var/www/html/yazilim_egitim_blog/bootstrap/cache directory must be present and writable. </br>

sudo chmod -R 775 bootstrap/cache/ </br></br>

## 6- SQLSTATE[HY000]General Error: 8 attempt to write a readonly database</br>

sudo chmod -R 775 database </br></br>

## 7- termiminalde laravel not found icin php dockerfile dosyalarina asagidakini ekle </br>

ENV PATH="/root/.composer/vendor/bin:${PATH}"</br></br>

## 8- ek bilgi </br>

sudo usermod -aG www-data okanaras </br>

umask olayı ise; projeleriniz /home/okanaras/my-projects/projects içinde. Öyleyse projects klasöründe iken mesela şöyle yaparsanız: </br>

'$ umask 022' </br>
'$ git clone git@github.com:username/test-project.git' </br>

Klon işlemi test-project diye bir klasör oluştururken önce umask 022 yaptığınız için dosya ve klasörleri doğru okuma yazma izinleri ile oluşturur. Yapmazsanız git içinde tanımlı izinler ile oluşturur ve daha sonra o dosyalarda düzenleme yapamazsınız.</br></br>
