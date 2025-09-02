
> **TypeScript ile JavaScript kodlarının birlikte sorunsuz şekilde çalışabilmesidir.**  
> Bu sayede projene yavaş yavaş TS dosyaları ekleyebilir veya dış kütüphaneleri (npm ile gelen saf JS kodları) TypeScript içinde kullanabilirsin.

---

## 📌 Kullanım Senaryoları

|Senaryo|Açıklama|
|---|---|
|1.|Mevcut JS projesine `.ts` dosyaları eklemek|
|2.|JS dosyasını `.ts` içinden kullanmak|
|3.|JS modülü yazıp TS içinde çağırmak|
|4.|TS modülünü JS içinde çağırmak|
|5.|TS dışı npm kütüphanelerine tip tanımı eklemek (`@types/...`)|

---

## ✅ 1. JavaScript dosyasını TypeScript içinde kullanma

### `math.js`

```js
function add(a, b) {
  return a + b;
}
module.exports = { add };
```

### `main.ts`

```ts
// JS dosyasını import edebilirsin
const { add } = require('./math');
console.log(add(2, 3)); // 5
```

🧠 Ama dikkat: TypeScript burada `add` fonksiyonunun tipini bilemez. Bu yüzden gerekirse **manual type declaration** eklersin:

```ts
declare function add(a: number, b: number): number;
```

---

## ✅ 2. JavaScript projesine TypeScript dosyası eklemek

JS projen varsa ve yavaş yavaş TypeScript’e geçmek istiyorsan:

1. `tsconfig.json` dosyasını oluştur:
    

```bash
tsc --init
```

2. `allowJs` ayarını aç:
    

```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": false,  // istersen true yapıp JS dosyalarını da kontrol ettirirsin
    "outDir": "./dist"
  },
  "include": ["src/**/*"]
}
```

3. `.ts` dosyalarını yazmaya başla. Eski `.js` dosyaları da çalışır.
    

---

## ✅ 3. Dış JavaScript kütüphanesini TypeScript ile kullanma

### Örnek: Lodash

```bash
npm install lodash
npm install --save-dev @types/lodash
```

### Kullanım:

```ts
import _ from 'lodash';

const numbers = [1, 2, 3];
console.log(_.shuffle(numbers)); // [2, 1, 3] gibi
```

👉 `@types/lodash` olmasaydı, TS bu kütüphanenin fonksiyonlarını tanıyamazdı.

---

## ✅ 4. `.d.ts` ile JavaScript'e tip tanımı eklemek

### `legacy.js`

```js
function multiply(a, b) {
  return a * b;
}
```

> TS bunu tanımaz. Biz `.d.ts` (declaration file) ile tipi elle tanımlarız:

### `legacy.d.ts`

```ts
declare function multiply(a: number, b: number): number;
```

### `main.ts`

```ts
/// <reference path="./legacy.d.ts" />
console.log(multiply(2, 4)); // 8
```

---

## ✅ 5. TypeScript modülünü JavaScript içinde kullanmak

### `sum.ts`

```ts
export function sum(a: number, b: number): number {
  return a + b;
}
```

### `main.js`

```js
const { sum } = require("./dist/sum");
console.log(sum(10, 5));
```

> Not: `.ts` dosyası derlendikten sonra oluşan `.js` çağrılır (`tsc` ile derlemeyi unutma).

---

## 🎁 Ekstra: Mixed Project Önerisi

```text
project/
├── tsconfig.json
├── src/
│   ├── helpers.ts
│   ├── math.js
│   ├── main.ts
│   └── legacy.d.ts
```

---

## 🚨 Dikkat Edilmesi Gerekenler

|Uyarı|Açıklama|
|---|---|
|JS modüllerini doğru `require` / `import` et|ESModules vs CommonJS farkı önemli|
|Tip kontrolü JS'de yoktur|`checkJs: true` yapsan bile eksik kalır|
|`@types` paketleri kritik|Tip desteği olmayan npm paketleri için gereklidir|
|Karmaşık geçişte `allowJs` + `isolatedModules` kullan|Geçici çözüm ama dikkatli ol!|

---

## 🎯 Özet

|Başlık|Bilgi|
|---|---|
|✅ JS içinde TS kullanılır mı?|Derlenmiş halinden evet|
|✅ TS içinde JS kullanılır mı?|Evet, ama tip desteği istenirse elle eklenmeli|
|✅ NPM JS paketleri TS’te kullanılır mı?|Evet, `@types` paketi varsa daha rahat|
|✅ Eski JS projesi TS’e taşınır mı?|Adım adım taşınabilir (`allowJs` + `tsconfig`)|

---

Hazırsan sıradaki konuya geçebiliriz:  
👉 **TypeScript Temel Tipler (number, string, boolean, any, unknown, void, never)** konusuna başlayalım mı?

Yoksa yukarıdaki interoperability konusundan özel örnek ya da kullanım senaryosu istiyor musun?