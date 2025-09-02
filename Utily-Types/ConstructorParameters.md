
## 🔹 `ConstructorParameters<T>` Nedir?

`ConstructorParameters<T>` → Bir **class constructor’ının parametre tiplerini tuple** olarak çıkarır.

- Fonksiyon versiyonu olan `Parameters<T>`’in constructor versiyonudur.
- `T` → constructor tipi (`new (...args: any) => any`)

📌 Tanımı (TypeScript içinde):

```ts
type ConstructorParameters<T extends abstract new (...args: any) => any> =
  T extends abstract new (...args: infer P) => any ? P : never;
```

- `infer P` → constructor parametrelerini yakalar
- `T` bir constructor değilse → `never`

---

## 🔹 Örnekler

### 1. Basit class constructor

```ts
class User {
  constructor(public id: number, public name: string, public age: number) {}
}

type UserParams = ConstructorParameters<typeof User>;
// type UserParams = [id: number, name: string, age: number]
```

---

### 2. Parametresiz constructor

```ts
class Config {
  constructor() {}
}

type ConfigParams = ConstructorParameters<typeof Config>;
// type ConfigParams = []
```

---

### 3. Opsiyonel ve default parametreler

```ts
class Product {
  constructor(public name: string, public price?: number) {}
}

type ProductParams = ConstructorParameters<typeof Product>;
// type ProductParams = [name: string, price?: number | undefined]
```

---

### 4. Gerçek kullanım (dynamic instantiation)

```ts
class Car {
  constructor(public brand: string, public model: string) {}
}

type CarParams = ConstructorParameters<typeof Car>;

function createInstance<T extends new (...args: any) => any>(
  ctor: T,
  ...args: ConstructorParameters<T>
) {
  return new ctor(...args);
}

const myCar = createInstance(Car, "BMW", "M5");
console.log(myCar.brand); // BMW
```

---

### 5. `never` dönen durum

```ts
type NotClass = string;

type Params = ConstructorParameters<NotClass>;
// type Params = never
```

Çünkü `string` bir class constructor değil.

---

## 🔹 Kullanım Senaryoları

- **Factory fonksiyonları** yazarken constructor parametrelerini tip güvenli almak.
- **Dependency Injection** sistemlerinde class’ları dinamik oluşturmak.
- **Dynamic object creation** için parametreleri tuple olarak almak.

---

✅ Özet:

- `ConstructorParameters<T>` → bir class constructor’ının **parametre tiplerini tuple olarak** verir.
- Fonksiyon versiyonu: `Parameters<T>`
- Kullanım alanı: **factory**, **dynamic instantiation**, **dependency injection**.
