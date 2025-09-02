
## 🔹 `Pick<T, K>` Nedir?

`Pick<T, K>` bir tipten **sadece belirli property’leri seçip** yeni bir tip oluşturur.

- `T` → Kaynak tip (örnek: `User`)
- `K` → Seçilecek property’lerin isimleri (`keyof T` tipinde olmalı)

---

## 🔹 Genel Kullanım

```ts
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};
```

- `keyof T` → T tipindeki tüm property anahtarlarını temsil eder.
- `K extends keyof T` → sadece mevcut property’ler seçilebilir.
- `Pick` sonucu → seçilen property’lerden oluşan yeni tip.

---

## 🔹 Örnek

```ts
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}

// Sadece id ve name alanlarını seçiyoruz
type UserSummary = Pick<User, "id" | "name">;

const user1: UserSummary = {
  id: 1,
  name: "TkMatE"
};

// user1.email ❌ yok çünkü Pick sadece id ve name içeriyor
```

---

## 🔹 Kullanım Senaryoları

### 1. API DTO Oluşturma

Bazen API’de kullanıcıya sadece belirli alanları göstermek istersin.  
Örn: kullanıcı bilgileri → şifre gibi hassas alanlar hariç tutulur.

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

type PublicUserDto = Pick<User, "id" | "name" | "email">;

const safeUser: PublicUserDto = {
  id: 1,
  name: "TkMatE",
  email: "tkmate@test.com"
};
// password yok ❌
```

---

### 2. Kısmi Veri Modeli Kullanma

Bir tablonun veya objenin sadece küçük bir kısmını işlemek istediğinde.

```ts
interface Product {
  id: number;
  title: string;
  price: number;
  stock: number;
}

type ProductPreview = Pick<Product, "title" | "price">;

const item: ProductPreview = {
  title: "Laptop",
  price: 25000
};
```

---

### 3. Generic Fonksiyonlarda Kullanım

`Pick` ile bir objeden sadece lazım olan alanları çekebilirsin.

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): Pick<T, K> {
  return { [key]: obj[key] } as Pick<T, K>;
}

const user: User = { id: 1, name: "TkMatE", email: "a@test.com", age: 23 };

const picked = getProperty(user, "email");
console.log(picked); // { email: "a@test.com" }
```

---

✅ Özet:

- `Pick<T, K>` → T tipinden **K alanlarını seçip yeni bir tip** oluşturur.
- Kullanım alanları: **API DTO’ları**, **public/private data ayrımı**, **yalnızca gerekli alanları kullanmak**.
