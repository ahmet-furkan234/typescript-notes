
`keyof`, bir nesne tipinin **tüm anahtarlarını (property name)** bir **union type** olarak döndüren bir **TypeScript type operatörüdür**.

---

## 📌 Temel Söz Dizimi

```ts
type Person = {
  name: string;
  age: number;
};

type PersonKeys = keyof Person;
// PersonKeys = "name" | "age"
```

Yani `keyof` sayesinde tip seviyesinde `"name"` veya `"age"` gibi string literal tiplerini elde ederiz.

---

## 🧠 Ne İşe Yarar?

- Daha **genel ve esnek** generic yapılar kurmakta
- **Dinamik olarak erişilen property’leri** güvenli hale getirmekte
- **Map/Filter gibi generic fonksiyonlar** yazarken kritik rol oynar

---

## 🔍 Detaylı Örnekler

### ✅ 1. Basit Kullanım

```ts
type Car = {
  brand: string;
  year: number;
};

type CarKeys = keyof Car; 
// => "brand" | "year"
```

### ✅ 2. Fonksiyon İçinde Kullanımı

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { id: 1, name: "TkMatE" };
const userId = getProperty(user, "id"); // ✅ tip: number
const userName = getProperty(user, "name"); // ✅ tip: string
// getProperty(user, "email"); ❌ Error: "email" 'user' objesinde yok
```

---

### ✅ 3. Union ile `keyof` Kullanımı

```ts
type Settings = {
  theme: "dark" | "light";
  notifications: boolean;
};

type SettingKeys = keyof Settings;
// => "theme" | "notifications"
```

---

### ✅ 4. Dinamik Property Kontrolü (Güvenli `Object.keys`)

TypeScript `Object.keys()` fonksiyonunun dönüş tipini `string[]` olarak bilir, ama biz bunu daha güvenli hale getirebiliriz:

```ts
function typedKeys<T>(obj: T): (keyof T)[] {
  return Object.keys(obj) as (keyof T)[];
}

const person = { name: "Ahmet", age: 30 };
const keys = typedKeys(person); // type: ("name" | "age")[]
```

---

### ✅ 5. `typeof` ile Kombine Kullanımı

```ts
const settings = {
  resolution: "1080p",
  fps: 60
};

type SettingsKeys = keyof typeof settings;
// => "resolution" | "fps"
```

---

## 🔄 `keyof` ve `typeof` Beraberliği

|Kullanım|Açıklama|
|---|---|
|`typeof obj`|Değişkenin tipini alır (`obj`’nin tipi)|
|`keyof typeof obj`|Objeye ait tüm key'lerin union tipini çıkarır|

---

## 🔐 Advanced: `Record` ile `keyof` Kullanımı

```ts
type LanguageCodes = "en" | "tr" | "de";

const translations: Record<LanguageCodes, string> = {
  en: "Hello",
  tr: "Merhaba",
  de: "Hallo"
};

function translate(lang: keyof typeof translations) {
  return translations[lang];
}
```

---

## 🚧 Edge Case: Nested `keyof`

```ts
type Nested = {
  user: {
    name: string;
    email: string;
  };
};

type Level1 = keyof Nested;         // "user"
type Level2 = keyof Nested["user"]; // "name" | "email"
```

---

## 🎯 Özet

|Özellik|Açıklama|
|---|---|
|`keyof T`|T tipi içindeki tüm property adlarını union olarak verir|
|`K extends keyof T`|`T` tipindeki bir objenin yalnızca geçerli key'lerini temsil eder|
|Güçlü yönü|Dinamik key erişimini **type-safe** hale getirir|
|Kullanım alanı|Generic fonksiyonlar, form validasyonları, UI maper'ları|
