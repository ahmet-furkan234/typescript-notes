
## 🔹 `Omit<T, K>` Nedir?

`Omit<T, K>` → Bir tipten **belirli property’leri çıkarıp** yeni bir tip oluşturur.

- `T` → Kaynak tip
- `K` → Çıkarılacak property’ler (`keyof T` tipinde olmalı)

📌 `Pick<T, K>` seçmek için kullanılırken, `Omit<T, K>` **çıkarmak** için kullanılır.

---

## 🔹 Genel Kullanım

```ts
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
```

- `keyof T` → T’nin tüm property isimleri
- `Exclude<keyof T, K>` → çıkarılacak property’leri ayıklar
- Sonuç: `Pick` ile kalan property’lerden yeni tip oluşturulur

---

## 🔹 Örnek

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

// password'u çıkardık
type PublicUser = Omit<User, "password">;

const u: PublicUser = {
  id: 1,
  name: "TkMatE",
  email: "tkmate@test.com"
};
// u.password ❌ yok
```

---

## 🔹 Kullanım Senaryoları

### 1. Hassas Alanları Çıkarmak (DTO için ideal)

```ts
interface Employee {
  id: number;
  name: string;
  salary: number;
  ssn: string; // sosyal güvenlik no
}

// API response’ta ssn göstermeyelim
type PublicEmployee = Omit<Employee, "ssn">;

const e: PublicEmployee = { id: 1, name: "Ali", salary: 5000 };
```

---

### 2. Update / Create DTO Ayırma

Bazen **create** sırasında tüm alanlar gerekir ama **update** için bazı alanlar hariç tutulur.

```ts
interface Product {
  id: number;
  title: string;
  price: number;
  stock: number;
}

type CreateProductDto = Omit<Product, "id">; // id otomatik üretilir
type UpdateProductDto = Partial<Omit<Product, "id">>; // id hariç opsiyonel update
```

---

### 3. Birden Fazla Alanı Çıkarmak

Birden fazla property çıkarmak için `|` kullanılır.

```ts
interface Car {
  id: number;
  brand: string;
  model: string;
  price: number;
}

type CarPreview = Omit<Car, "id" | "price">;

const car: CarPreview = {
  brand: "BMW",
  model: "M5"
};
```

---

## 🔹 `Pick` ve `Omit` Karşılaştırma

- `Pick<T, K>` → sadece istediğin alanları seçersin.
- `Omit<T, K>` → sadece istemediğin alanları çıkartırsın.

```ts
interface User {
  id: number;
  name: string;
  email: string;
}

// Aynı sonuç:
type ByPick = Pick<User, "id" | "name">;
type ByOmit = Omit<User, "email">;
```

---

✅ Özet:

- `Omit<T, K>` → T tipinden **K alanlarını çıkartarak** yeni tip oluşturur.
- Kullanım alanları: **hassas verileri ayırma**, **create/update DTO oluşturma**, **fazlalıkları temizleme**.
