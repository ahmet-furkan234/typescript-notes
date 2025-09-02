
## 🔷 1. Konu Tanımı

JavaScript kütüphaneleri (örneğin `express`, `lodash`, `jquery`, vs.) **TypeScript ile yazılmadığı** için içinde **tip bilgisi (type information)** bulunmaz.

TypeScript ile bu kütüphaneleri kullanabilmek için dışarıdan bu tip bilgilerini sağlayan paketlere ihtiyaç duyarız. Bu paketler:

- `@types/` ile başlar
- `DefinitelyTyped` adlı açık kaynak havuzdan gelir
- Geliştirme ortamında kullanılır (çalışma zamanında etkisi yoktur)

---

## 🎯 2. Neden Type Definitions Kullanılır?

|Amaç|Açıklama|
|---|---|
|✅ IntelliSense|Kod tamamlama ve açıklamalar otomatik gelir|
|✅ Hata önleme|Yanlış parametre/veri tipi kullanıldığında TS uyarır|
|✅ Derleme hataları|Yanlış API kullanımı build-time’da fark edilir|
|✅ Refactor kolaylığı|IDE üzerinden güvenle yeniden düzenleme yapılabilir|

---

## 🛠️ 3. DefinitelyTyped ve `@types` Nedir?

### ✅ DefinitelyTyped:

- Açık kaynaklı, GitHub üzerindeki bir depo
- JavaScript kütüphaneleri için yazılmış **topluluk destekli tip tanımlarını** içerir
- Adres: [https://github.com/DefinitelyTyped/DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)

### ✅ @types:

- DefinitelyTyped üzerindeki tanımların npm paketi halidir.
- `@types/express`, `@types/jquery`, `@types/lodash` gibi isimlerle gelir.
- Bu paketler sadece **geliştirme sırasında** kullanılır.

---

## 📦 4. Kurulum Komutu

### Genel Format:

```bash
npm install -D @types/<paket-ismi>
```

|Parça|Açıklama|
|---|---|
|`npm install`|Paket yükle|
|`-D` veya `--save-dev`|Geliştirme bağımlılığı olarak kur|
|`@types/<paket>`|Tip tanımı paketi|

### Örnekler:

```bash
npm install express
npm install -D @types/express
```

```bash
npm install lodash
npm install -D @types/lodash
```

---

## 💡 5. Örnek Kod ile Açıklama

### Önce Kurulum:

```bash
npm install express
npm install -D @types/express
```

### Sonra TypeScript Kodu:

```ts
import express from 'express';

const app = express();

app.get('/', (req, res) => {
    res.send("Merhaba TkMatE!");
});
```

### Faydası:

- `req`, `res`, `app.get` gibi öğelerin tüm tipi bellidir
- IntelliSense otomatik çalışır
- Yanlış parametre girilirse TypeScript uyarır

---

## 🔄 6. Geliştirme ve Üretim Ortamları

|Ortam|Tip Tanımları Gerekli mi?|Açıklama|
|---|---|---|
|Geliştirme|✅ Evet|Kod yazarken TypeScript'e yardımcı olur|
|Üretim (build sonrası)|❌ Hayır|Derlenmiş JavaScript dosyasında gerekmez|

---

## 🧩 7. @types Paketi Gerektirmeyen Durumlar

Bazı kütüphaneler zaten **TypeScript ile yazılmıştır**, bu durumda ekstra `@types` paketine gerek kalmaz. Örneğin:

- `axios` ✅ kendi tipleriyle birlikte gelir
- `nestjs` ✅ zaten TS ile yazılmıştır

Kontrol etmek için:

```bash
npm info axios types
```

---

## 🚫 8. Tip Tanımı Olmayan Kütüphaneler

Eğer bir kütüphane için `@types/<paket>` bulunmuyorsa:

- `any` türünde kullanılır (TypeScript bu modülün detayını bilemez)
- Geçici çözüm: kendi tip tanımını elle yazmak

Örnek:

```ts
// typings.d.ts
declare module 'kütüphane-ismi';
```

---

## 📌 9. package.json'da Nasıl Görünür?

```json
"devDependencies": {
  "@types/node": "^20.8.3",
  "@types/express": "^4.17.21"
}
```

> Bu paketler `node_modules` içinde yer alır ve sadece geliştirme sırasında aktiftir.

---

## 🧠 10. Kısa Özet

|Konu|Açıklama|
|---|---|
|`@types/`|JavaScript kütüphanelerinin TypeScript tipi|
|`DefinitelyTyped`|Bu tanımların tutulduğu GitHub deposu|
|`npm install -D @types/...`|Tip paketini geliştirme ortamı için yükle|
|Avantaj|Hata önleme, IntelliSense, güvenli kodlama|

---

İstersen bu konuyu Obsidian için şu başlıkla kaydedebilirsin:

> ## 🧩 TypeScript – Using Type Definitions with JavaScript Libraries (`@types`)
