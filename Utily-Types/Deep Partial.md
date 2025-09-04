
### 🔑 `Partial` ve `DeepPartial` Arasındaki Fark

- **`Partial<T>`** → Yüzeysel (shallow) çalışır.  
    Sadece **ilk seviyedeki** property’leri opsiyonel yapar.
    - Nested objeler **hala zorunlu**.

- **`DeepPartial<T>`** → Derin (recursive) çalışır.  
    Tüm **nested objeler dahil** bütün property’leri opsiyonel yapar.
    - Güncellemelerde en çok tercih edilen yapı.


---

### 📖 Normal Anlatımı (Partial → DeepPartial Farkı)

```ts
interface Address {
  city: string;
  street: string;
}

interface User {
  name: string;
  age: number;
  address: Address;
}
```

#### `Partial<User>` sonucu:

```ts
{
  name?: string;
  age?: number;
  address?: Address; // ❌ hala full Address bekler
}
```

#### `DeepPartial<User>` sonucu:

```ts
{
  name?: string;
  age?: number;
  address?: {
    city?: string;
    street?: string;
  }; // ✅ her şey opsiyonel
}
```

---

### 🛠 Kullanım Senaryosu

- **`Partial`** → Genellikle DTO’larda (update gibi basit durumlarda ama nested yoksa) işine yarar.
- **`DeepPartial`** → Update işlemleri için **nested objeler** olduğunda daha mantıklı.

Örn: Senin güncelleme JSON’un:

```json
{
  "location": { "city": "Ankara" },
  "contacts": { "email": "hello@techhub.com" }
}
```

- `Partial` ile hata çıkar.
- `DeepPartial` ile gayet doğal çalışır.

---

### 🧩 Pratik Tip Tanımı

```ts
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};
```

---



### 📦 Kullanabileceğin Paketler

#### 1. **type-fest** → En çok kullanılan

```bash
npm install type-fest
```

Kullanım:

```ts
import { PartialDeep } from "type-fest";

interface User {
  name: string;
  address: {
    city: string;
    street: string;
  };
}

type UserUpdate = PartialDeep<User>;

const u: UserUpdate = {
  address: { city: "Ankara" } // ✅ sadece city gönderebilirsin
};
```

---

#### 2. **ts-essentials**

```bash
npm install ts-essentials
```

Kullanım:

```ts
import { DeepPartial } from "ts-essentials";

interface User {
  name: string;
  address: {
    city: string;
    street: string;
  };
}

type UserUpdate = DeepPartial<User>;
```

---

#### 3. **utility-types**

```bash
npm install utility-types
```

Kullanım:

```ts
import { DeepPartial } from "utility-types";

type UserUpdate = DeepPartial<User>;
```

---

Yani özetle:  
- 👉 `Partial` sadece yüzeysel → shallow  
- 👉 `DeepPartial` recursive → nested her alan opsiyonel

---
### ✅ Önerim

- En güncel ve kapsamlı paket: **`type-fest`**
- Eğer projende sadece `DeepPartial` lazım → `ts-essentials` daha hafif.
