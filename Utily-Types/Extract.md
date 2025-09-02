
## 🔹 `Extract<T, U>` Nedir?

`Extract<T, U>` → Bir **union type** içinden sadece **ortak (kesişim) tipleri alır**.

- `T` → kaynak tip
- `U` → filtrelenecek tip(ler)

📌 Yani `T ∩ U` işlemini yapar (küme kesişimi gibi düşünebilirsin).

---

## 🔹 Genel Kullanım

```ts
type Extract<T, U> = T extends U ? T : never;
```

- Eğer `T`, `U`’ya atanabilirse → `T` kalır
- Değilse → `never` (atılır)

---

## 🔹 Örnek

```ts
type Roles = "admin" | "editor" | "user";
type Allowed = "editor" | "user" | "guest";

// Kesişim: editor ve user
type FinalRoles = Extract<Roles, Allowed>;
// "editor" | "user"
```

---

## 🔹 Kullanım Senaryoları

### 1. Union’dan Ortak Alanları Bulmak

```ts
type Status = "active" | "inactive" | "pending" | "banned";
type PublicStatus = "active" | "inactive" | "pending";

type ValidStatus = Extract<Status, PublicStatus>;
// "active" | "inactive" | "pending"
```

---

### 2. Enum ile Kullanım

```ts
enum PaymentMethod {
  Cash = "cash",
  CreditCard = "credit_card",
  Paypal = "paypal"
}

type OnlinePayments = Extract<PaymentMethod, PaymentMethod.Paypal | PaymentMethod.CreditCard>;
// "credit_card" | "paypal"
```

---

### 3. String Literal Filtreleme

```ts
type AllKeys = "id" | "name" | "email" | "password";
type SafeKeys = "id" | "name" | "email";

type PublicKeys = Extract<AllKeys, SafeKeys>;
// "id" | "name" | "email"
```

---

### 4. API DTO Senaryosu

Backend’den gelen tipten sadece güvenli alanları almak için kullanılabilir.

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

type AllowedKeys = Extract<keyof User, "id" | "name" | "email">;
// "id" | "name" | "email"

type PublicUser = Pick<User, AllowedKeys>;
```

---

## 🔹 `Extract` ile `Exclude` Karşılaştırma

- `Exclude<T, U>` → `T`’den `U`’yu **çıkartır**.
- `Extract<T, U>` → `T` ile `U`’nun **kesişimini alır**.

```ts
type A = "a" | "b" | "c";
type B = "b" | "c" | "d";

type Ex1 = Exclude<A, B>; // "a"
type Ex2 = Extract<A, B>; // "b" | "c"
```

---

✅ Özet:

- `Extract<T, U>` → `T` union tipinden sadece `U` ile ortak olanları alır.
- Kullanım alanları: **union kesişimi**, **enum filtreleme**, **güvenli DTO alanları seçme**.
