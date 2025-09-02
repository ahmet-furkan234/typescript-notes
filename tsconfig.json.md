
> `tsconfig.json`, TypeScript projesinin yapılandırma dosyasıdır.  
> Projenin **hangi dosyalarının derleneceğini**, **derleme sonucunun nasıl olacağını** ve **hangi kuralların geçerli olacağını** belirler.

---

## 🧩 Temel `tsconfig.json` Yapısı

```json
{
  "compilerOptions": {
    // Derleyici ayarları buraya
  },
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules"
  ]
}
```

---

## 🔧 `compilerOptions` - En Önemli Ayarlar

|Ayar|Açıklama|
|---|---|
|`target`|Derlenecek JS çıktısının versiyonu (`ES5`, `ES6`, `ESNext` vs.)|
|`module`|Modül sistemi (`commonjs`, `es6`, `umd`, `amd`)|
|`outDir`|Derlenen dosyaların çıkış klasörü|
|`rootDir`|Kaynak TypeScript dosyalarının kök dizini|
|`strict`|Tüm sıkı kuralları açar (`true` önerilir)|
|`esModuleInterop`|CommonJS modüllerini ES modül gibi kullanmaya izin verir|
|`allowJs`|`.js` dosyalarının da derlenmesine izin verir|
|`checkJs`|`.js` dosyalarında da hata kontrolü yapar|
|`sourceMap`|`.js.map` dosyaları üretilir (debug için)|
|`declaration`|`.d.ts` tip tanım dosyaları üretir|
|`noImplicitAny`|Tip belirtilmeyen yerlerde `any` kullanımına hata verir|
|`noEmit`|Derleme çıktısı üretmeden sadece kontrol yapar|

---

## ✅ Örnek: Modern ve Sıkı Konfigürasyon

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true,
    "outDir": "./dist",
    "rootDir": "./src"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

---

## 🔍 Açıklamalı Versiyon

```json
{
  "compilerOptions": {
    "target": "ES6",                      // Çıktı JS hangi sürüm? (ES5, ES6, ES2020...)
    "module": "commonjs",                 // Modül sistemi (Node.js için commonjs)
    "rootDir": "./src",                   // TS kaynakları nerede?
    "outDir": "./dist",                   // JS çıktıları nereye?
    "strict": true,                       // Tüm sıkı denetimleri aktif eder
    "esModuleInterop": true,              // `require` vs `import` uyumu
    "skipLibCheck": true,                 // @types kütüphanelerindeki hataları atla
    "forceConsistentCasingInFileNames": true  // Büyük/küçük harf uyumsuzluklarını önler
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

---

## 💡 Ekstra Özellikler

### 🔹 `lib`

Kullanılacak yerleşik API’leri belirler:

```json
"lib": ["ES2020", "DOM"]
```

> Örneğin sadece tarayıcı projesi yapıyorsan `DOM`, `ES6` yeterli.

---

### 🔹 `paths` & `baseUrl` (Alias kullanımı)

```json
"baseUrl": "./src",
"paths": {
  "@utils/*": ["utils/*"]
}
```

Kullanım:

```ts
import { helper } from "@utils/helper";
```

---

### 🔹 `allowJs` + `checkJs`

```json
"allowJs": true,
"checkJs": true
```

> `.js` dosyalarını da projeye dahil eder ve tip kontrolü yapar.  
> JavaScript’ten TypeScript’e geçiş sürecinde çok kullanışlıdır.

---

### 🔹 `declaration`

```json
"declaration": true
```

> Derleme sırasında `.d.ts` dosyası da üretir.  
> Bu dosyalar, başka projelerin senin modüllerini kullanabilmesini sağlar.

---

## 🛠 Komutlar

|Amaç|Komut|
|---|---|
|`tsconfig.json` oluştur|`npx tsc --init`|
|Projeyi derle|`npx tsc`|
|İzleyerek derle|`npx tsc --watch`|

---

## 📁 Örnek Proje Yapısı

```text
my-project/
├── src/
│   └── index.ts
├── dist/
├── tsconfig.json
├── package.json
```

---

## 🧠 Özet

|Konu|Açıklama|
|---|---|
|`tsconfig.json`|Derleyici yapılandırma dosyasıdır|
|`compilerOptions`|Derleme kurallarını tanımlar|
|`include/exclude`|Hangi dosyalar derlenecek? Hangileri hariç?|
|`strict: true`|Güvenli kod için mutlaka önerilir|
|`paths/baseUrl`|Alias ile import düzeni sağlanır|

---

İstersen birlikte bir `tsconfig.json` dosyası yazabiliriz, ya da  
👉 Şimdi sıradaki konu olan **TypeScript Temel Tipler (number, string, boolean, any, void, never, unknown)** konusuna geçelim mi?