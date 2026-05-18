# ✦ Yıldız Galaksisi — Deployment Kılavuzu

## Vercel ile Yayına Alma (5 dakika)

### 1. GitHub'a Yükle
1. [github.com](https://github.com) → yeni repo oluştur → "yildiz-galaksisi"
2. Bu iki dosyayı yükle: `index.html` ve `vercel.json`

### 2. Vercel'e Bağla
1. [vercel.com](https://vercel.com) → Google/GitHub ile ücretsiz kayıt
2. "Add New Project" → GitHub repoyu seç
3. "Deploy" butonuna tıkla — otomatik build edilir
4. Siteniz `yildiz-galaksisi.vercel.app` adresinde yayında!

### 3. Özel Domain (isteğe bağlı)
- Vercel dashboard → Settings → Domains
- `yildizgalaksisi.com` gibi bir domain ekle
- Domain sağlayıcında DNS ayarlarını Vercel'e yönlendir

---

## OKX Sipariş Takibi (Manuel Doğrulama)

Müşteri sipariş verdiğinde:
1. OKX cüzdanınızı kontrol edin (TRC-20 / ERC-20 / BTC vb.)
2. Tutar ve açıklama eşleşiyor mu kontrol edin
3. Eşleşiyorsa sertifikayı oluşturun ve e-posta gönderin

### Cüzdan Adreslerini Değiştirme
`index.html` içinde şu bölümü bulun:

```js
const addresses = {
  'USDT-TRC20': 'TQzeMBdK9b7rEHTTVZMVFkRo7RuWpKZGfQ',  ← KENDİ ADRESİNİZ
  'USDT-ERC20': '0x3Fa4B0E5...',                         ← KENDİ ADRESİNİZ
  'BTC': 'bc1qxy2kgd...',                                ← KENDİ ADRESİNİZ
  'ETH': '0x3Fa4B0E5...',                                ← KENDİ ADRESİNİZ
  'BNB': 'bnb1grpf09...'                                 ← KENDİ ADRESİNİZ
};
```

Bu adresleri kendi OKX cüzdan adreslerinizle değiştirin.

---

## Sipariş Bildirimi İçin (Formspree - Ücretsiz)

Müşteri "Siparişi Onayla" dediğinde e-posta almak için:

1. [formspree.io](https://formspree.io) → ücretsiz kayıt
2. Yeni form oluştur → form ID'nizi alın (örn: `xpwzabcd`)
3. `index.html` içinde `submitOrder()` fonksiyonunu bulun ve şu kodu ekleyin:

```js
async function submitOrder() {
  const payload = {
    plan: currentPlan,
    price: currentPrice,
    coin: currentCoin,
    name: document.querySelector('input[placeholder*="isim"]').value,
    email: document.querySelector('input[type="email"]').value,
    message: document.querySelector('textarea').value
  };

  await fetch('https://formspree.io/f/FORM_ID_BURAYA', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  });

  alert('✦ Teşekkürler! Ödemeniz doğrulandıktan sonra sertifikanız gönderilecektir.');
  closeModal();
}
```

---

## Destek
Herhangi bir adımda takılırsanız Claude'a sorun!
