
## 🔹 `Awaited<T>` Nedir?

`Awaited<T>` → Bir tipin **Promise çözülmüş değerini** verir.

- Eğer tip zaten Promise değilse, aynen geri döner.
- Eğer tip **nested Promise** ise (örn: `Promise<Promise<T>>`) → en derin değeri alır.

📌 Tanımı (TypeScript içinde):

```ts
type Awaited<T> = T extends null | undefined
  ? T
  : T extends object & { then(onfulfilled: infer F, ...args: any): any }
    ? F extends (value: infer V, ...args: any) => any
      ? Awaited<V>
      : never
    : T;
```

- Yani tip Promise mi değil mi kontrol eder ve **resolve edilmiş tip**i çıkarır.

---

## 🔹 Örnekler

### 1. Basit Promise

```ts
type P = Promise<number>;

type Result = Awaited<P>;
// type Result = number
```

---

### 2. Nested Promise

```ts
type P = Promise<Promise<string>>;

type Result = Awaited<P>;
// type Result = string
```

---

### 3. Normal tip

```ts
type A = string;

type Result = Awaited<A>;
// type Result = string (değişmez)
```

---

### 4. Async fonksiyon ile kullanım

```ts
async function fetchData() {
  return { data: [1, 2, 3] };
}

type DataType = Awaited<ReturnType<typeof fetchData>>;
// type DataType = { data: number[] }
```

- `ReturnType<typeof fetchData>` → `Promise<{ data: number[] }>`
- `Awaited` → `{ data: number[] }`

---

### 5. Daha karmaşık kullanım

```ts
type NestedPromise = Promise<Promise<Promise<boolean>>>;

type Final = Awaited<NestedPromise>;
// type Final = boolean
```

---

## 🔹 Kullanım Senaryoları

- **Async/await fonksiyonlarının dönüş tiplerini almak**
- **Promise tiplerini çözerek tip güvenliği sağlamak**
- **Nested Promise durumlarında tipi normalize etmek**

---

✅ Özet:

- `Awaited<T>` → T tipi Promise ise **resolve edilmiş tipi**, değilse aynısını verir.
- Özellikle `ReturnType` ile birlikte async fonksiyonlarda çok kullanışlıdır.
