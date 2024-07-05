
### GPG Anahtar Oluşturma ve Git ile Kullanma

#### 1\. GPG Anahtar Oluşturma

  1. **GPG'yi Yükleyin:**

     * **Windows:** [Gpg4win](https://gpg4win.org/) indirin ve yükleyin.
     * **MacOS:** Terminal'de `brew install gnupg` komutunu çalıştırın.
     * **Linux:** Terminal'de `sudo apt-get install gnupg` (Debian tabanlı) veya `sudo yum install gnupg` (Red Hat tabanlı) komutunu çalıştırın.
  2. **GPG Anahtarınızı Oluşturun:**
    

    
    
    
    gpg --full-generate-key
    

     * `RSA and RSA` (default) seçeneğini seçin.
     * Anahtar uzunluğunu (2048 veya 4096) seçin.
     * Anahtarın ne kadar süre geçerli olacağını belirleyin (örneğin, 0=sonsuza kadar).
     * Adınızı, e-posta adresinizi ve isteğe bağlı bir yorumu girin.
     * Şifrenizi belirleyin.
  3. **GPG Anahtarınızın Kimliğini Görüntüleyin:**
    

    
    
    
    gpg --list-secret-keys --keyid-format LONG
    

     * `sec` satırında yer alan `4096R/` ile başlayan uzun kimliği (örneğin, `4096R/ABCDEFGHIJKLMNO`) not edin.
  4. **GPG Anahtarınızı Kopyalayın:**
    

    
    
    
    gpg --armor --export <KEY_ID>
    

     * `<KEY_ID>` yerine yukarıda not ettiğiniz uzun kimliği (sadece harf ve rakamlar) kullanın.
     * Çıktıyı kopyalayın.

#### 2\. GitHub'a GPG Anahtarınızı Ekleyin

  1. **GitHub'da Giriş Yapın:** [GitHub](https://github.com/) hesabınıza giriş yapın.

  2. **GPG Anahtarını Ekleyin:**

     * Profilinizde sağ üst köşede bulunan kullanıcı simgenize tıklayın ve `Settings`'i seçin.
     * Sol menüde `SSH and GPG keys`'e tıklayın.
     * `New GPG key` butonuna tıklayın ve kopyaladığınız GPG anahtarını yapıştırın.
     * `Add GPG key` butonuna tıklayın.

#### 3\. Git İmzalama Yapılandırması

  1. **Git Yapılandırmasını Güncelleyin:**
    

    
    
    
    git config --global user.signingkey <KEY_ID>
    git config --global commit.gpgSign true
    

  2. **GitHub için GPG Agent Yapılandırması (Opsiyonel):** Eğer GPG agent kullanıyorsanız, aşağıdaki komutu ekleyin:
    

    
    
    
    echo "use-agent" >> ~/.gnupg/gpg.conf
    echo "pinentry-mode loopback" >> ~/.gnupg/gpg.conf
    

### SSH Anahtar Oluşturma ve GitHub ile Kullanma

#### 1\. SSH Anahtar Oluşturma

  1. **SSH Anahtarınızı Oluşturun:**
    

    
    
    
-keygen -t rsa -b 4096 -C "your_email@example.com"
    

     * `your_email@example.com` yerine GitHub hesabınızla ilişkili e-posta adresinizi kullanın.
     * Varsayılan dosya konumunu kullanabilir ve isterseniz bir parola belirleyebilirsiniz.
  2. **SSH Anahtarınızı Kopyalayın:**
    

    
    
    
/id_rsa.pub
    

     * Çıktıyı kopyalayın.

#### 2\. GitHub'a SSH Anahtarınızı Ekleyin

  1. **GitHub'da Giriş Yapın:** [GitHub](https://github.com/) hesabınıza giriş yapın.

  2. **SSH Anahtarını Ekleyin:**

     * Profilinizde sağ üst köşede bulunan kullanıcı simgenize tıklayın ve `Settings`'i seçin.
     * Sol menüde `SSH and GPG keys`'e tıklayın.
     * `New SSH key` butonuna tıklayın ve kopyaladığınız SSH anahtarını yapıştırın.
     * `Add SSH key` butonuna tıklayın.

#### 3\. Git İçin SSH Anahtarını Kullanma

  1. **SSH Ajanını Başlatın ve Anahtarı Ekleyin:**
    

    
    
    
-agent -s)"
/id_rsa
    

  2. **Git Remote URL'sini SSH ile Değiştirin:** Mevcut HTTP/S URL'lerini SSH ile değiştirmek için:
    

    
    
    
    git remote set-url origin git@github.com:username/repository.git
    

Bu rehberi izleyerek GPG ve SSH anahtarlarınızı oluşturabilir, GitHub ile
kullanabilir ve commitlerinizi doğrulayabilirsiniz.

