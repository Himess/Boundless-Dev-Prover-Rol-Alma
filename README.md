# Boundless Dev & Prover Rolü Alma Rehberi

![image](https://github.com/user-attachments/assets/7baa366f-c773-47e3-b13e-b80b0e2ca877)

Bu rehberde Boundless testnet üzerinde Dev ve Prover rollerini almak için gerekli tüm adımlar yer almaktadır.

Öncelikle Bu roller ‘ in herhangi bir teşviği açıklanmadı ve garantisi yoktur. Kendim aldım ve sizinle paylaşmak istedim.
Eğer daha önce hiç bir node kurulumu vs. gerçekleştirmediyseniz zorlanabilirsiniz. Lakin elimden geldiğinice basit bir şekilde anlatmaya çalıştım.

Ben M2 air kullancısıyım. Kendi pc' me kurulumu yaptım. İsterseniz VPS kiralayıp işlemleri yapabilirsiniz. Linux/M1/M3 için aynıdır diye tahmin ediyorum. Farklı olabilecek yerleri belirrtim.
Tabi bir de Sepolia ETH almayı da unutmayın.

## ÖNEMLİ UYARI !!! Burada Metamask için kullanacağınız cüzdanın testnet cüzdanı olmasını şiddetle tavsiye ederim. Priv key kullanacağımız için pc’de depolanması sıkıntılar yaratabilir. Boş bir metamask adresi işinizi görecektir.

Öncelikle gereklilikler

1- 6 ay’dan daha eski bir Discord hesabı

2- 6 ay’dan daha eski bir Github hesabı

Daha sonra bize 2 şey lazım.

1 - Testnet Metamask Adresimiz. 
2- Infura ‘ dan alacağımız Sepolia eth RPC url


## METAMASK İÇİN 

Sağ üstten üç noktaya tıklayıp hesap bilgilerine tıklayın.

![image](https://github.com/user-attachments/assets/e796eae9-3934-4430-8670-c5716b9b6184)

Daha sonra özel anahtarı göstere tıklayın ve size verdiği anahtarı bir not defterine kaydedin bize lazım olacak.

## INFURA İÇİN

https://developer.metamask.io/register adresine git. Burada kayıt ol / giriş yap.

![Developer](https://github.com/user-attachments/assets/22f37d7b-f907-42d8-b849-dc6927bb2796)

Sol’dan Infura RPC ‘ ye tıkla.

Size böyle bir key verecek.

<img width="910" alt="Mask" src="https://github.com/user-attachments/assets/80f11acb-bb99-4c32-b522-c96b6c601c16" />

Bu keyi de bir yere not edin.

Tamam her şey hazır şimdi kuruluma geçebiliriz.

---

## 🧱 1. Boundless Repo'sunu Klonla

```bash
git clone https://github.com/boundless-xyz/boundless
cd boundless
git checkout release-0.10
```

---

## 🦀 2. Rust Kurulumu

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Kurulum sırasında şu çıkarsa:

1) Proceed with installation (default)

→ `1` yazıp Enter'a bas.

Sonrasında:

```bash
source $HOME/.cargo/env
```

---

## ⚙️ 3. RISC Zero Kurulumu

```bash
curl -L https://risczero.com/install | bash
source ~/.zshrc
rzup install
```

Eğer `source ~/.zshrc` hata verirse `source ~/.bashrc` yazın.

---

## 📦 4. Bento Client Kurulumu

```bash
cargo install --git https://github.com/risc0/risc0 bento-client --bin bento_cli
export PATH="$HOME/.cargo/bin:$PATH"
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Bunda da aynı şekilde eğer hata alırsanız 

`echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.zshrc`  yerine `echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc`
`source ~/.zshrc`yerine `source ~/.bashrc`

---

## 🚀 5. Boundless CLI Kurulumu

```bash
cargo install --locked boundless-cli
```

---

## 🧾 6. .env.base Dosyasını Oluştur

Aşağıdaki komutla dosyayı aç:

```bash
nano .env.base
```

En altına şunları ekle (kendi bilgilerinle değiştir):
Burada en başta aldığımız infura rpc ve priv keyi girin.

```bash
export ETH_RPC_URL="https://base-mainnet.infura.io/v3/<senin_project_id>"
export PRIVATE_KEY="<test_cüzdanının_private_key>"
```

Örnek tüm dosya:

```bash
export VERIFIER_ADDRESS=0x925d8331ddc0a1F0d96E68CF073DFE1d92b69187
export BOUNDLESS_MARKET_ADDRESS=0x13337C76fE2d1750246B68781ecEe164643b98Ec
export SET_VERIFIER_ADDRESS=0x7aAB646f23D1392d4522CFaB0b7FB5eaf6821d64
export ORDER_STREAM_URL="https://eth-sepolia.beboundless.xyz/"
export ETH_RPC_URL="https://base-mainnet.infura.io/v3/xxxxx"
export PRIVATE_KEY="abc..."
```

export ORDER_STREAM_URL="https://eth-sepolia.beboundless.xyz/" Bunu ellemeyin , bu olduğu gibi kalsın.

Kaydetmek için:
Control X + Y Enter

Sonrasında:

```bash
source .env.base
```

---

## 💰 7. BASE Mainnet USDC 10 USDC AL.

https://app.uniswap.org/swap ' gir ve Base Mainnet'te En az 10 USDC al.

---

## 🪙 8. Stake İşlemi Yap

USDC geldiğinde aşağıdaki komutu çalıştır:

```bash
boundless \
  --rpc-url "$ETH_RPC_URL" \
  --private-key "$PRIVATE_KEY" \
  --boundless-market-address 0x26759dbB201aFbA361Bec78E097Aa3942B0b4AB8 \
  --set-verifier-address 0x8C5a8b5cC272Fe2b74D18843CF9C3aCBc952a760 \
  --verifier-router-address 0x0b144e07a0826182b6b59788c34b32bfa86fb711 \
  --order-stream-url https://base-mainnet.beboundless.xyz \
  account deposit-stake 10
```

Başarılı çıktı şu şekilde olur:

![Pasted Graphic 11](https://github.com/user-attachments/assets/a666856a-52dc-4797-8e95-bdbbeb1f6ed7)

## 🪙 9. Deposit İşlemi Yap

```bash
boundless \
  --rpc-url "$ETH_RPC_URL" \
  --private-key "$PRIVATE_KEY" \
  --boundless-market-address 0x26759dbB201aFbA361Bec78E097Aa3942B0b4AB8 \
  --set-verifier-address 0x8C5a8b5cC272Fe2b74D18843CF9C3aCBc952a760 \
  --verifier-router-address 0x0b144e07a0826182b6b59788c34b32bfa86fb711 \
  --order-stream-url "https://base-mainnet.beboundless.xyz" \
  account deposit 0.00000000001
```

Başarılı çıktı şu şekilde olur:

![image](https://github.com/user-attachments/assets/1d4c1782-ab72-45d0-a56e-a8fe9c2ac31e)

---

## 🏅 10. Rolünü Al

1. Git: https://guild.xyz/boundless-xyz  
2. Sayfayı yenile → cüzdanını bağla  
3. Eğer stake ve deposit işlemi algılanırsa `Dev` ve `Prover` rozetleri aktifleşir  
4. Ardından Discord’da `#claim-dev-prover-roles` kanalına git → “Claim the Prover role on Guild.xyz” ve “Claim the Dev role on Guild.xyz” butonuna tıkla.

![Claim the Prover rele](https://github.com/user-attachments/assets/f977bc53-dab0-4c61-90a2-5c872e4eb88b)

![We have updated your accesses](https://github.com/user-attachments/assets/87815cf0-f957-4c6a-8e24-d99f9dfd7817)

🎉 Tebrikler! Artık Boundless Dev & Prover rollerine sahipsin!

Thanks to @Miles082510 and @0xMoei

Eğer komple prover node kurmak isterseniz 
📚 Daha fazla teknik detay için: [@0xMoei'nin Boundless Node Kurulum Rehberi](https://github.com/0xmoei/boundless/)

