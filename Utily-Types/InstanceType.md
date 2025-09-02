
## 🔹 `InstanceType<T>` Nedir?

`InstanceType<T>` → Bir **class tipi** alır ve bu class’tan **oluşacak instance’ın tipini** verir.

- `T` → class constructor tipi (`new (...args: any) => any`)

📌 Tanımı (TypeScript içinde):

```ts
type InstanceType<T extends new (...args: any) => any> =
    T extends new (...args: any) => infer R ? R : any;
```

- `infer R` → constructor tarafından oluşturulan nesnenin tipini yakalar.
- Fonksiyon değilse `any` veya `never` dönebilir.

---

## 🔹 Örnekler

### 1. Basit class

```ts
class User {
  constructor(public id: number, public name: string) {}
}

type UserInstance = InstanceType<typeof User>;
// type UserInstance = User

const u: UserInstance = new User(1, "TkMatE");
console.log(u.name); // TkMatE
```

---

### 2. Parametresiz class

```ts
class Config {
  apiUrl = "http://localhost";
}

type ConfigInstance = InstanceType<typeof Config>;
// type ConfigInstance = Config

const cfg: ConfigInstance = new Config();
console.log(cfg.apiUrl); // http://localhost
```

---

### 3. Factory ile kullanım

```ts
function createInstance<T extends new (...args: any) => any>(
  ctor: T,
  ...args: ConstructorParameters<T>
): InstanceType<T> {
  return new ctor(...args);
}

const carInstance = createInstance(class Car {
  constructor(public brand: string, public model: string) {}
}, "BMW", "M5");

console.log(carInstance.brand); // BMW
```

---

### 4. `never` dönen durum

```ts
type NotClass = string;

type Instance = InstanceType<NotClass>;
// type Instance = never
```

Çünkü `string` bir class constructor değil.

---

## 🔹 Kullanım Senaryoları

- **Dynamic factory fonksiyonları** yazarken tip güvenliği sağlamak.
- **Dependency injection** sistemlerinde class instance tipini almak.
- `ConstructorParameters` + `InstanceType` kombinasyonu ile **dinamik object creation** yapmak.

---

✅ Özet:

- `InstanceType<T>` → class constructor tipinden **instance tipini** çıkarır.
- Kullanım alanları: **factory**, **dependency injection**, **dynamic instantiation**.
