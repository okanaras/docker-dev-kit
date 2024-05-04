### Docker Quick Start

1.  Kurulum icin:

        wsl --install

2.  Varsayilan distro atama.

        wsl --list
        wsl --setdefault DISTRO-NAME -> wsl --setdefault Ubuntu

3.  Ubuntu güncellemelerimizi ve gerekli paketlerimizi kuralım.

        sudo apt update
        sudo apt upgrade -y
        sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

4.  NodeJS kurulumu

        sudo apt-get update
        sudo apt-get install -y ca-certificates curl gnupg
        sudo mkdir -p /etc/apt/keyrings
        curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

        NODE*MAJOR=20
        echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node*$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

        sudo apt-get update
        sudo apt-get install nodejs -y

5.  Alternative node npm kurulumu

        sudo apt update -y
        sudo apt upgrade -y
        sudo apt-get install nodejs -y
        sudo apt install npm -y

6.  WSL Kaldirma

        wsl --list
        wsl --unregister Ubuntu

7.  Github Kurulumu

        sudo apt install git
        git --version
        git config --global user.name "Okan Aras"
        git config --global user.email "oknaras@icloud.com"
        git config --global init.defaultBranch main
        cat ~/.gitconfig

8.  SSH kurulumu

        ssh-keygen -t rsa -b 4096 -C "okanaras"
        code ~//.ssh/id_rsa.pub

        ssh -T git@github.com
        yes

9.  Docker Desktop

        General bölümünde 'Use WSL 2 ve Use Docker Compose V2' seçili olsun.
        Resources -> WSL Integration bölümünde Ubuntu seçeneğini aktif edelim.
        Nginx default.conf'ta ayaga kalkacak path, domain ve php surumunu veriyoruz
        Ardindan ../etc/hosts hosts dosyasina ayni domaini veriyoruz

        docker-compose up -d ile ayaga kaldiriyoruz
        docker ps ile container lari listeliyoruz
        docker exec -it <cont_id> bash baglaniyoruz

        docker-compose stop
        docker-compose down
        docker-compose up -d --build
        docker-compose build --no-cache

10. laravel .env de

        app_url="url", (http://project.test)
        db_host=mysql, (yml icinde verilen ad)
        db_password="pass" (12345678)

11. vscode permission hatasi

        sudo chown -R okanaras /home/okanaras
        sudo chown -R okanaras:okanaras

12. The stream or file "/var/www/html/yazilim_egitim_blog/storage/logs/laravel.log" could not be opened in append

        sudo chmod -R 777 storage/

13. The /var/www/html/yazilim_egitim_blog/bootstrap/cache directory must be present and writable.

        sudo chmod -R 777 bootstrap/cache/

14. SQLSTATE[HY000]General Error: 8 attempt to write a readonly database

        sudo chmod -R 777 database

15. Termiminalde laravel not found icin php klasorlerindeki dockerfile dosyalarina asagidakini ekle

        ENV PATH="/root/.composer/vendor/bin:${PATH}"

16. Ek bilgi

        sudo usermod -aG www-data okanaras

        umask olayı ise; projeleriniz /home/okanaras/my-projects/projects içinde.
        Öyleyse projects klasöründe iken mesela şöyle yaparsanız:

        '$ umask 022'
        '$ git clone git@github.com:username/test-project.git'

        Klon işlemi test-project diye bir klasör oluştururken önce umask 022 yaptığınız için dosya ve klasörleri doğru okuma yazma izinleri ile oluşturur.
        Yapmazsanız git içinde tanımlı izinler ile oluşturur ve daha sonra o dosyalarda düzenleme yapamazsınız.
