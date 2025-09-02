
## 🔹 `ReturnType<T>` Nedir?

`ReturnType<T>` → Bir **fonksiyon tipinin dönüş tipini** alır.

- Yani bir fonksiyonun return ettiği değerin tipini otomatik olarak çıkarır.
- `T` → fonksiyon tipi (`(...args: any) => any`)

📌 Tanımı (TypeScript içinde):

```ts
type ReturnType<T extends (...args: any) => any> =
    T extends (...args: any) => infer R ? R : any;
```

- `infer R` → fonksiyonun return tipini yakalar
- Fonksiyon değilse `any` veya `never` dönebilir

---

## 🔹 Örnekler

### 1. Basit fonksiyon

```ts
function sum(a: number, b: number) {
  return a + b;
}

type SumReturn = ReturnType<typeof sum>;
// type SumReturn = number
```

---

### 2. String döndüren fonksiyon

```ts
function greet(name: string) {
  return `Hello, ${name}`;
}

type GreetReturn = ReturnType<typeof greet>;
// type GreetReturn = string
```

---

### 3. Void döndüren fonksiyon

```ts
function logMessage(msg: string) {
  console.log(msg);
}

type LogReturn = ReturnType<typeof logMessage>;
// type LogReturn = void
```

---

### 4. Promise döndüren fonksiyon

```ts
async function fetchData() {
  return { data: [1, 2, 3] };
}

type FetchReturn = ReturnType<typeof fetchData>;
// type FetchReturn = Promise<{ data: number[] }>
```

---

### 5. Fonksiyon tipinden return tipini çıkarma

```ts
type FnType = (a: string, b: string) => boolean;

type ResultType = ReturnType<FnType>;
// type ResultType = boolean
```

---

## 🔹 Kullanım Senaryoları

- **Wrapper fonksiyonlar** yazarken tip güvenliği sağlamak:

```ts
function wrapper<T extends (...args: any) => any>(fn: T): ReturnType<T> {
  // do something
  return fn(...([] as Parameters<T>));
}
```

- **API response tiplerini** otomatik almak:

```ts
async function getUser() {
  return { id: 1, name: "TkMatE" };
}

type UserResponse = ReturnType<typeof getUser>;
// Promise<{ id: number, name: string }>
```

- **Dinamik fonksiyon çağrılarında** return tipi garantisi sağlamak.

---

✅ Özet:

- `ReturnType<T>` → Fonksiyon tipinin **dönüş tipini** verir.
- Kullanım alanları: **wrapper fonksiyonlar**, **API response tipleri**, **tip güvenli çağrılar**.
