
## 🔹 `Required<T>` Nedir?

`Partial<T>`’in tam tersidir.  
Bir tipin **tüm property’lerini zorunlu** (`required`) hale getirir.

---

## 🔹 Genel Kullanım

```ts
type Required<T> = {
  [P in keyof T]-?: T[P];
};
```

Buradaki `-?` ifadesi property’den **opsiyonelliği kaldırır**.  
Yani varsa `?`, hepsini zorunlu hale getirir.

---

## 🔹 Örnek

```ts
interface User {
  id: number;
  name?: string;
  email?: string;
}

let u1: User = { id: 1 }; // geçerli çünkü name ve email opsiyonel

let u2: Required<User> = {
  id: 1,
  name: "TkMatE",
  email: "test@test.com"
}; 
// tüm alanlar zorunlu oldu
```

---

## 🔹 Kullanım Senaryoları

### 1. DTO’yu zorunlu hale getirmek

Bazen bir tipin opsiyonel alanları olabilir ama belirli bir yerde **her şeyin doldurulması gerektiğini** isteyebilirsin.

```ts
interface Config {
  host?: string;
  port?: number;
  secure?: boolean;
}

function connect(config: Required<Config>) {
  console.log(
    `Connecting to ${config.host}:${config.port}, secure=${config.secure}`
  );
}

connect({ host: "localhost", port: 3000, secure: true }); // ✅ tüm alanlar şart
```

---

### 2. Partial + Required Kombinasyonu

Mesela update sırasında bazı alanlar opsiyonel ama backend tarafında **hepsini zorunluya çevirip işlem yapmak** isteyebilirsin.

```ts
interface User {
  id: number;
  name?: string;
  email?: string;
}

type UpdateUserDto = Partial<User>;

function processUpdate(data: Required<UpdateUserDto>) {
  // burada tüm alanların geleceği garanti
  console.log(data.id, data.name, data.email);
}
```

---

## 🔹 `Required<T>` ile Normal Tip Arasındaki Fark

- `interface` tanımında `?` varsa opsiyoneldir.
- `Required<T>` ile bunlar kaldırılır.

```ts
interface A {
  x: number;
  y?: number;
}

type B = Required<A>; // hem x hem y zorunlu
```

---

✅ Özet:

- `Required<T>` → T’nin tüm property’lerini **zorunlu** yapar.
- En çok **config yapılarında** veya **opsiyonel tipleri kesinleştirmek** istediğimizde kullanılır.
