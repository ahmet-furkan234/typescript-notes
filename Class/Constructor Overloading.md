
> Aynı sınıfta birden fazla `constructor` tanımlayarak, nesne oluşturulurken farklı parametrelerle farklı davranışlar gösterebilmeyi sağlar.

TypeScript'te:

- **birden fazla imza** (signature) tanımlayabiliriz,
- ama sadece **bir adet gerçek `constructor` gövdesi (body)** yazabiliriz.

---

## 🔹 1. Temel Constructor Overloading Örneği

```ts
class User {
  name: string;
  age: number;

  // Overload imzaları
  constructor(name: string);
  constructor(name: string, age: number);

  // Tek bir uygulama (gövde)
  constructor(name: string, age?: number) {
    this.name = name;
    this.age = age ?? 0;
  }

  info() {
    console.log(`${this.name} - ${this.age}`);
  }
}

const u1 = new User("TkMatE");
const u2 = new User("TkMatE", 30);

u1.info(); // TkMatE - 0
u2.info(); // TkMatE - 30
```

### ✅ Açıklamalar:

- İlk iki `constructor(...)` → sadece imza, yani overload tanımıdır.
- Alttaki `constructor(...)` → gerçek kodu içeren tek constructor’dır.
- `age?: number` sayesinde age opsiyonel olur.
- `??` nullish coalescing: `undefined` ise `0` atanır.

---

## 🔹 2. Farklı Türlerle Overload

```ts
class Logger {
  message: string;

  constructor(msg: string);
  constructor(code: number);
  constructor(param: string | number) {
    if (typeof param === "string") {
      this.message = `Log: ${param}`;
    } else {
      this.message = `Error Code: ${param}`;
    }
  }

  print() {
    console.log(this.message);
  }
}

const l1 = new Logger("Başarıyla kaydedildi");
const l2 = new Logger(404);

l1.print(); // Log: Başarıyla kaydedildi
l2.print(); // Error Code: 404
```

---

## 🔹 3. Object Parametresi ile Esnek Overloading

```ts
interface UserOptions {
  name: string;
  age?: number;
}

class FlexibleUser {
  name: string;
  age: number;

  constructor(name: string);
  constructor(options: UserOptions);
  constructor(param: string | UserOptions) {
    if (typeof param === "string") {
      this.name = param;
      this.age = 0;
    } else {
      this.name = param.name;
      this.age = param.age ?? 0;
    }
  }

  info() {
    console.log(`${this.name} - ${this.age}`);
  }
}

const fu1 = new FlexibleUser("TkMatE");
const fu2 = new FlexibleUser({ name: "TkMatE", age: 24 });

fu1.info(); // TkMatE - 0
fu2.info(); // TkMatE - 24
```

> Bu tarz constructor overloading, özellikle opsiyonel `DTO`'lar ve `config` nesneleri için çok uygundur.

---

## 🔹 4. Overload’larla Hatalı Kullanım

Aşağıdaki gibi **birden fazla gövdeli constructor yazılamaz**:

```ts
class X {
  constructor(a: string) { }      // ✅
  // constructor(b: number) { }   // ❌ HATA: Sadece 1 gövde yazılabilir
}
```

---

## 📌 Tip İpuçları

- `param: string | number` → union type ile overload gövdesi yazılır
- `typeof` veya `instanceof` → parametre türü kontrolü yapılır
- `??`, `||` → default değerler atanabilir

---

## 🔚 Özet

|Özellik|Açıklama|
|---|---|
|Çoklu imza tanımı|Evet (sadece imza, gövde içeremez)|
|Tek bir gerçek constructor gövdesi|Evet (zorunlu)|
|`typeof`, `instanceof` ile kontrol|Gerekli|
|DTO-like yapı desteği|Object overload ile mümkün|
