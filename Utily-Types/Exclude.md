
## 🔹 `Exclude<T, U>` Nedir?

`Exclude<T, U>` → Bir **union type** içinden **istenmeyen tipleri çıkarıp** yeni bir tip oluşturur.

- `T` → kaynak tip
- `U` → çıkarılacak tip(ler)

📌 Yani `T` ∖ `U` işlemini yapar (küme farkı gibi düşünebilirsin).

---

## 🔹 Genel Kullanım

```ts
type Exclude<T, U> = T extends U ? never : T;
```

- Eğer `T`, `U`’ya atanabilirse → `never` (yok edilir)
- Değilse → `T` kalır

---

## 🔹 Örnek

```ts
type Roles = "admin" | "editor" | "user";

// "editor" çıkarılıyor
type WithoutEditor = Exclude<Roles, "editor">;

// eşdeğer: "admin" | "user"
```

---

## 🔹 Kullanım Senaryoları

### 1. Union’dan İstenmeyenleri Çıkarmak

```ts
type Status = "active" | "inactive" | "pending" | "banned";

type PublicStatus = Exclude<Status, "banned">;
// "active" | "inactive" | "pending"
```

---

### 2. Tip Kombinasyonlarında Filtreleme

```ts
type Primitive = string | number | boolean | null | undefined | object;

// object dışındaki basit tipleri seçtik
type OnlyPrimitives = Exclude<Primitive, object>;
// string | number | boolean | null | undefined
```

---

### 3. Enum ile Kullanım

```ts
enum LogLevel {
  Debug = "debug",
  Info = "info",
  Warn = "warn",
  Error = "error"
}

type NonDebugLevels = Exclude<LogLevel, LogLevel.Debug>;
// "info" | "warn" | "error"
```

---

### 4. Omit ile Birlikte Kullanım

`Omit<T, K>` zaten `Exclude` kullanılarak implement edilmiştir.  
Çünkü `Omit`, `Pick` + `Exclude` kombinasyonudur:

```ts
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
```

Yani aslında `Exclude` → `Omit` ve `Extract` gibi utility’lerin temel yapı taşıdır.

---

## 🔹 `Exclude` ile `Extract` Farkı

- `Exclude<T, U>` → T’den U’yu çıkarır
- `Extract<T, U>` → T ile U’nun kesişimini alır

```ts
type A = "a" | "b" | "c";
type B = "b" | "c" | "d";

type OnlyA = Exclude<A, B>; // "a"
type Common = Extract<A, B>; // "b" | "c"
```

---

✅ Özet:

- `Exclude<T, U>` → `T` union tipinden `U`’yu çıkarır.
- Kullanım alanları: **union filtreleme**, **enum temizleme**, **istenmeyen tipleri ayıklama**.
