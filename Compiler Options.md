

## ✅ Temel `compilerOptions` Ayarları

### 1. `target`

> Derlenecek JavaScript kodunun hangi sürümde üretileceğini belirler.

```json
"target": "ES6"
```

|Seçenek|Açıklama|
|---|---|
|ES3 / ES5|Eski tarayıcılar için|
|ES6 (ES2015)|Modern tarayıcılar için standart|
|ES2020 / ESNext|Yeni JS özellikleri için|

---

### 2. `module`

> Hangi modül sistemini kullanacağını belirler (import/export sistemleri).

```json
"module": "commonjs"
```

|Seçenek|Nerede kullanılır|
|---|---|
|commonjs|Node.js|
|es6/esnext|Web ve modern tarayıcılar|
|amd / umd|Eski tarayıcılar, RequireJS ortamları|

---

### 3. `rootDir` & `outDir`

> Derleme sırasında kaynak ve çıktı klasörlerini belirler.

```json
"rootDir": "./src",
"outDir": "./dist"
```

---

### 4. `strict`

> Tek bir ayarla birçok sıkı kuralı açar. Gelişmiş TypeScript için önerilir.

```json
"strict": true
```

Açtığı ayarlar:

- `noImplicitAny`
- `strictNullChecks`
- `strictFunctionTypes`
- `strictBindCallApply`
- `strictPropertyInitialization`
- `alwaysStrict`

---

## ✅ Güvenlik ve Tip Denetimi

### 5. `noImplicitAny`

> Tip belirtilmeyen yerlerde `any` olmasına hata verir.

```json
"noImplicitAny": true
```

```ts
function greet(name) { } // ❌ Hata (name: any oldu)
```

---

### 6. `strictNullChecks`

> `null` ve `undefined` değerlerinin kontrol edilmesini zorunlu kılar.

```json
"strictNullChecks": true
```

```ts
let x: string = null; // ❌ Hata
```

---

### 7. `noImplicitReturns`

> Fonksiyonun her yoldan `return` döndürmesini ister.

```json
"noImplicitReturns": true
```

```ts
function f(x: number) {
  if (x > 5) return "ok";
} // ❌ Hata: her yol return içermiyor
```

---

### 8. `noFallthroughCasesInSwitch`

> `switch` deyiminde `case`'lerin arasına `break` koymazsan uyarır.

```json
"noFallthroughCasesInSwitch": true
```

---

## ✅ JavaScript Uyumluluğu

### 9. `allowJs`

> `.js` dosyalarını derlemeye dahil eder.

```json
"allowJs": true
```

### 10. `checkJs`

> `.js` dosyalarında da tip denetimi yapar (sadece `allowJs: true` ile çalışır).

```json
"checkJs": true
```

---

## ✅ Modül Kullanımı ve Uyumluluk

### 11. `esModuleInterop`

> CommonJS modüllerini `import` ile uyumlu hale getirir.

```json
"esModuleInterop": true
```

```ts
import express from 'express'; // ✔️ olur
```

### 12. `moduleResolution`

> Modül dosyaları nasıl bulunacak?

```json
"moduleResolution": "node"
```

---

## ✅ Gelişmiş Ayarlar

### 13. `declaration`

> Derleme sırasında `.d.ts` tip tanım dosyaları üretir (kütüphane yazıyorsan şart).

```json
"declaration": true
```

### 14. `sourceMap`

> JS içinde TS’ye geri izleme sağlar. Debug için çok yararlıdır.

```json
"sourceMap": true
```

---

### 15. `removeComments`

> Derleme sonucu JS dosyasında yorumları siler.

```json
"removeComments": true
```

---

### 16. `noEmit`

> Dosya üretmeden sadece hataları kontrol eder.  
> CI/CD ya da sadece statik analiz için kullanılır.

```json
"noEmit": true
```

---

## ✅ paths & baseUrl (Alias)

```json
"baseUrl": "./src",
"paths": {
  "@utils/*": ["utils/*"]
}
```

> Şöyle kullanırsın:

```ts
import { log } from "@utils/logger";
```

---

## ✅ Özet Tablo

|Ayar|Açıklama|Öneri|
|---|---|---|
|`target`|Çıktı JS versiyonu|`"ES6"` veya `"ES2020"`|
|`module`|Modül sistemi|`"commonjs"` (Node), `"esnext"` (Web)|
|`strict`|Tüm sıkı kurallar|`true` ✅|
|`outDir` / `rootDir`|Dosya yolları|`"dist"` / `"src"`|
|`esModuleInterop`|`require`/`import` uyumu|`true` ✅|
|`allowJs` / `checkJs`|JS dosya uyumluluğu|Geçiş sürecinde yararlı|
|`paths` / `baseUrl`|Alias kullanımı|Projelerde düzen sağlar|
|`declaration`|`.d.ts` dosyası üret|Kütüphane projelerinde şart|
