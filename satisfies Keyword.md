
`satisfies`, bir değerin **belirli bir tipe uygun olup olmadığını kontrol eder**, **ancak türünü değiştirmez**.

> 📌 **Amaç:** Derleyiciye "bu değişken bu tipi sağlıyor mu" diye doğrulama yaptırmak ama `as` gibi type cast yapmak değil.

---

## 📌 Neden Kullanılır?

- `as` operatörü gibi **zorlama type assertion** yerine **gerçek tip doğruluğu** sağlar.
- Literal değerlerin kendi türlerini korurken bir interface veya type şartlarını sağlamasını kontrol eder.

---

## 🧪 Temel Örnek:

```ts
type Point = { x: number; y: number };

const p1 = { x: 10, y: 20 } satisfies Point; ✅ // Doğru

const p2 = { x: 10 } satisfies Point; ❌ // HATA: y eksik
```

---

## 🔍 Farkı Nedir? (`satisfies` vs `as`)

|Özellik|`as`|`satisfies`|
|---|---|---|
|Tip doğrulama|Hayır (derleyici zorlanır)|Evet|
|Tip değiştirme|Evet|Hayır|
|Tip güvencesi|Düşük|Yüksek|

---

### 🔸 Örnek 2 – Literal değerlerin korunması

```ts
const obj = {
  role: "admin",
  level: 5
} satisfies { role: string; level: number };

// obj'nin türü: { role: "admin", level: 5 }
```

> Burada `"admin"` stringi **literal olarak korunur**, yani `"admin"` olarak kalır. `as` kullansaydın `"admin"` yerine `string` olurdu.

---

## ✅ `satisfies` ile Gerçek Hayat Kullanımı

### 📌 Örnek – Config Dosyası:

```ts
type Config = {
  port: number;
  env: "dev" | "prod";
};

const config = {
  port: 3000,
  env: "dev"
} satisfies Config;
```

> `config` nesnesi hem `Config` tipini sağlıyor, hem de property türleri korunuyor.

---

## 🛠️ Derin Örnek – keyof ile birlikte

```ts
const Routes = {
  home: "/",
  profile: "/user",
  settings: "/settings"
} satisfies Record<string, string>;

// Routes içindeki değerler string olmalı. Type kontrolü sağlanır.
```

---

## 🧩 Not: Type Narrowing için değil

`satisfies`, bir değişkenin türünü **daraltmak için kullanılmaz**. Bunun için `as`, `is`, type guards vb. kullanılır.

---

## 🎯 Özet

|Özellik|Açıklama|
|---|---|
|Amaç|Belirli bir tipin koşullarını sağlayıp sağlamadığını kontrol etmek|
|Tür değiştirir mi?|❌ Hayır, sadece kontrol eder|
|Derleyici güvencesi|✅ Çok yüksek|
|Ne zaman kullanılır?|Config dosyaları, sabit veri nesneleri, type güvenliği gerektiren durumlarda|

---

## 🧠 Tavsiyeler

- `as` yerine `satisfies` kullanmak daha **güvenli** ve **doğru** yaklaşımdır.
- Özellikle **literal korunması** gereken durumlarda büyük fark yaratır.
- TypeScript 4.9+ versiyon gerektirir.
