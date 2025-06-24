Bu repo tamamen 0xMoei ' nin github repodan video çekimi için alınmıştır. Kendisine teşekkür ederim. Detaylı rehber için burayı ziyaret edin. 
https://github.com/0xmoei/boundless/blob/main/README.md

# Otomatik Kurulum
Tüm bağımlılıkları, yapılandırmaları ve prover yönetimini otomatik olarak halleden bu script'i kullanarak kurulum yapabilirsiniz.

## Kurulum Script'ini İndirme ve Çalıştırma:
```bash
# Update packages
apt update && apt upgrade -y

# download wget
apt install wget
```

```bash
# Download the installation script
wget https://raw.githubusercontent.com/0xmoei/boundless/main/install_prover.sh -O install_prover.sh

# Make it executable
chmod +x install_prover.sh

# Run the installer
./install_prover.sh
```
*  Not: Kurulum uzun sürebilir çünkü bazı büyük dosyalar indiriliyor ve driver'lar kuruluyor. Endişe etmeyin.

  ###Kurulum Sırasında:
Script, GPU yapılandırmanızı otomatik olarak algılar.

Sizden aşağıdaki bilgiler istenir:

Ağ seçimi (mainnet/testnet)

RPC URL’si: Ayrıntılar için RPC Al kısmına bakın

Private key (gizli olarak girilir)

Broker yapılandırma parametreleri: Detayları için Broker Optimizasyonu kısmını ziyaret edin.


### Kurulum Sonrası Yönetim Script’i:
Kurulumdan sonra Prover’ınızı çalıştırmak veya yapılandırmak için kurulum klasörüne gidip `prover.sh` script’ini çalıştırmanız gerekir:

```bash
cd ~/boundless
./prover.sh
```

* [BlockPi](https://dashboard.blockpi.io/):

