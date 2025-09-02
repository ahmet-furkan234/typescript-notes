
## 🔹 `Record<K, T>` Nedir?

`Record<K, T>` → Bir tipin key’lerini (`K`) ve değer tipini (`T`) belirleyerek **yeni bir obje tip** oluşturur.

- `K` → key’lerin tipi (`string | number | symbol` veya union olabilir)
- `T` → value’ların tipi

📌 Yani `Record`, **belirli key’lerden oluşan bir obje** tanımlamaya yarar.

---

## 🔹 Genel Kullanım

```ts
type Record<K extends keyof any, T> = {
  [P in K]: T;
};
```

- `K` → property isimleri
- `T` → property değerlerinin tipi
- Her key aynı tipte value alır

---

## 🔹 Basit Örnek

```ts
type Roles = "admin" | "editor" | "user";

const permissions: Record<Roles, boolean> = {
  admin: true,
  editor: true,
  user: false
};
```

👉 Burada `permissions` objesinde `admin`, `editor`, `user` alanları **zorunlu** oldu ve hepsinin tipi `boolean`.

---

## 🔹 Kullanım Senaryoları

### 1. Key-Value Mapping

Bir objeyi sabit key’lerle ama tip güvenliğiyle tanımlamak için:

```ts
type Languages = "tr" | "en" | "de";

const translations: Record<Languages, string> = {
  tr: "Merhaba",
  en: "Hello",
  de: "Hallo"
};
```

Eğer `fr` eklemek istersek ❌ hata alırız çünkü `fr` `Languages` içinde yok.

---

### 2. ID → Nesne Mapleme

```ts
interface User {
  id: number;
  name: string;
}

const userMap: Record<number, User> = {
  1: { id: 1, name: "TkMatE" },
  2: { id: 2, name: "Ahmet" }
};
```

👉 Burada `userMap[1]` dediğinde otomatik olarak `User` tipinde veri gelir.

---

### 3. Dinamik Config Tanımları

```ts
type Environment = "dev" | "staging" | "prod";

interface Config {
  apiUrl: string;
  debug: boolean;
}

const configs: Record<Environment, Config> = {
  dev: { apiUrl: "http://localhost:3000", debug: true },
  staging: { apiUrl: "https://staging.api.com", debug: false },
  prod: { apiUrl: "https://api.com", debug: false }
};
```

---

### 4. Enum ile Kullanım

Enum değerlerini key olarak kullanabilirsin.

```ts
enum Status {
  Active = "active",
  Inactive = "inactive",
  Pending = "pending"
}

const statusMessages: Record<Status, string> = {
  [Status.Active]: "User is active",
  [Status.Inactive]: "User is inactive",
  [Status.Pending]: "User is pending approval"
};
```

---

## 🔹 `Record<K, T>` vs Normal Obje

- Normal obje yazarken yanlış key eklenebilir.
- `Record` → **tip güvenliği sağlar**, yanlış key veya value yazmana izin vermez.

---

✅ Özet:

- `Record<K, T>` → `K` key’lerini ve `T` value tiplerini zorunlu hale getirir.
- Kullanım alanları: **sözlük yapıları**, **çeviri sistemleri**, **config yönetimi**, **enum mapping**.
