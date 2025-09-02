
## 🔹 `NonNullable<T>` Nedir?

`NonNullable<T>` → Bir tipten **`null` ve `undefined` değerlerini çıkarır**.

- `T` → kaynak tip
- Sonuç → `T` içinden `null | undefined` hariç kalan tip

---

## 🔹 Genel Kullanım

```ts
type NonNullable<T> = T extends null | undefined ? never : T;
```

- Eğer `T` `null` veya `undefined` ise → `never` olur (atılır).
- Değilse → `T` kalır.

---

## 🔹 Örnek

```ts
type A = string | number | null | undefined;

type B = NonNullable<A>;
// string | number
```

---

## 🔹 Kullanım Senaryoları

### 1. Fonksiyon Dönüş Tiplerinde Null Safety

```ts
function findUser(id: number): string | null {
  return id === 1 ? "TkMatE" : null;
}

type UserName = NonNullable<ReturnType<typeof findUser>>;
// string
```

👉 Burada `findUser` normalde `string | null` dönerdi,  
ama `NonNullable` sayesinde `null` çıkarıldı → sadece `string` kaldı.

---

### 2. API Response Tiplerinden Temizlik

```ts
interface User {
  id: number;
  name: string | null;
  email?: string | null;
}

type SafeName = NonNullable<User["name"]>;   // string
type SafeEmail = NonNullable<User["email"]>; // string
```

---

### 3. Optional Parametrelerle Kullanım

```ts
type Params = string | undefined;

function printMessage(msg: NonNullable<Params>) {
  console.log(msg);
}

printMessage("Hello"); // ✅
// printMessage(undefined); ❌ Error
```

---

### 4. Union Tiplerde Kullanım

```ts
type Values = "a" | "b" | null | undefined;

type CleanValues = NonNullable<Values>;
// "a" | "b"
```

---

## 🔹 `NonNullable` vs `Exclude`

Aslında `NonNullable<T>`, `Exclude<T, null | undefined>` ile aynı anlama gelir.

```ts
type A = string | null | undefined;

type B = NonNullable<A>;
type C = Exclude<A, null | undefined>;

// B ve C tamamen aynı → string
```

---

✅ Özet:

- `NonNullable<T>` → `T` içinden **`null` ve `undefined`’ı çıkarır**.
- Kullanım alanları: **API response temizliği**, **fonksiyon dönüş tiplerinde null safety**, **optional parametrelerin garantiye alınması**.
