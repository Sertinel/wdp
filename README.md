# WDP (Web Developer Packs)

![Static Badge](https://img.shields.io/badge/WDP-online-green)

## Tavsiye Edilen Eklentiler

<img src="images/icon.png" alt="WDP Icon" style="width: 200px; height: auto; display: block; margin: 0 auto;" />

VS Code için derlenmiş eklenti paketi:
[WDP (Web Developer Packs)](https://github.com/Sertinel/wdp/releases/tag/v0.0.2)

---

### WDP Projesini Paketlemek İçin Kullanılacak Komutlar

Node.js yüklü olduğundan emin olduktan sonra aşağıdaki komutları kullanarak projenizi paketleyebilirsiniz:

```bash
# Önce vsce aracını globally olarak yükleyin
npm install -g @vscode/vsce

# Daha sonra eklentinizin bulunduğu klasöre gidin
cd myExtension

# Projeyi paketleyin
vsce package
# Bu komutla 'myExtension.vsix' dosyası oluşturulur

# Eklentinizi Visual Studio Code Marketplac'e yayınlayın
vsce publish
# Eklentiniz '<publisher id>.myExtension' olarak yayına alınır
```

---

### Fast Node Manager (fnm) ile Node.js Kurulumu

Öncelikle Windows için bir komut satırı yükleyicisi olan [`scoop`](https://scoop.sh)'u yüklememiz gerekiyor. Scoop sayesinde yükleme işlemleri daha temiz ve kolay olur.

#### 1. Yönetici Ayarına Geçme
Aşağıdaki komutla yönetici ayarına geçiyoruz:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### 2. Scoop Yükleme (Non-Admin)
Sistem yöneticisi olmadan (non-admin), varsayılan kurulum için aşağıdaki komutu kullanabilirsiniz:
```powershell
irm get.scoop.sh | iex
```

#### 3. fnm Yükleme
Scoop başarıyla kurulduysa, artık `fnm`'yi kurabilirsiniz:
```powershell
scoop install fnm
```

#### 4. PowerShell Profiline Kayıt Etme
Kurulum tamamlandıktan sonra `fnm`'yi her yerden kullanabilmeniz için PowerShell profiline kayıt eklememiz gerekiyor. Aksi takdirde `fnm --version` gibi komutlarda hata alabilirsiniz.

##### 1. Profil Oluşturma
Eğer daha önce bir profil oluşturulmadıysa yeni bir tane oluşturun:
```powershell
if (-not (Test-Path $profile)) { New-Item $profile -Force }
```

##### 2. Profil Dosyasını Açma
PowerShell profili (`Microsoft.PowerShell_profile.ps1`) dosyasını açmak için şu komutu çalıştırın:
```powershell
Invoke-Item $profile
```

##### 3. Gerekli Komutu Ekleme
Açılan `Microsoft.PowerShell_profile.ps1` dosyasının sonuna aşağıdaki satırı ekleyin ve dosyayı kaydedin:

```powershell
fnm env --use-on-cd --shell powershell | Out-String | Invoke-Expression
```

> Not: Eğer dosyanın içinde başka içerikler varsa, yeni satırı en alta ekleyin.

---

### Ekstra: `fnm` ile Kurulan Node.js'i PATH'e Ekleme

Eğer `fnm` ile kurduğunuz Node.js sürümü otomatik olarak PATH'e eklenmediyse, manuel olarak eklemek için aşağıdaki adımları izleyebilirsiniz.

#### 1. Mevcut PATH Değerini Görüntüleme
Bu komutla mevcut `PATH` ortam değişkeninin içeriğini görebilirsiniz:

```powershell
echo %PATH:;=&echo.%
```

#### 2. PATH'e Node.js Yolunu Ekleme
Kurduğunuz Node.js sürümünün yolunu `PATH` ortam değişkenine eklemek için aşağıdaki komutu kullanabilirsiniz. Bu örnekte varsayılan bir `fnm` kurulum yolu kullanılmıştır:

```powershell
setx path "%PATH%;C:\Users\User\AppData\Roaming\fnm\node-versions\v22.16.0\installation"
```

> ⚠️ **Not:**
> - `User`, bilgisayarınızın kullanıcı adıyla değiştirilmelidir.  
> - `v22.16.0`, kullandığınız Node.js sürümüne göre değişiklik gösterebilir.  
> - Bu işlem sadece **geçerli kullanıcı** için geçerlidir. Sistem genelinde yapmak isterseniz farklı bir yöntem kullanılmalıdır.

---

