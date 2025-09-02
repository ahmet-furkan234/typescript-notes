
## 🔷 1. Klasik Constructor Parametre Atama

```ts
class User {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}
```

### 🧠 Açıklama:

- `this.name = name` gibi atamalar tekrar gerektirir.
- Bu yöntem, büyük sınıflarda **gereksiz kod tekrarına** sebep olabilir.

---

## 🔷 2. Kısa Yol: Constructor Parameter Properties

```ts
class User {
  constructor(public name: string, public age: number) {}
}
```

### ✅ Bu yöntem ne sağlar?

- Otomatik olarak `this.name` ve `this.age` oluşturulur ve atanır.
- Kod daha kısa ve okunabilir olur.
- Yalnızca `constructor` parametresine `public`, `private`, `protected`, `readonly` gibi belirleyiciler eklemek yeterlidir.

---

## 🔷 3. Parametre Belirleyicileriyle Kullanım

|Belirleyici|Etkisi|
|---|---|
|`public`|Dışarıdan erişilebilir, örnek üzerinden ulaşılabilir|
|`private`|Sadece sınıf içinden erişilebilir|
|`protected`|Sınıf içinden ve alt sınıflardan erişilebilir|
|`readonly`|İlk atamadan sonra değiştirilemez|

```ts
class Product {
  constructor(
    public readonly id: number,
    private name: string,
    protected price: number
  ) {}

  getProductInfo(): string {
    return `${this.name} - $${this.price}`;
  }
}

const p = new Product(1, "Laptop", 1500);
console.log(p.id);             // ✅ id dışarıdan erişilebilir
console.log(p.getProductInfo()); // ✅ get methodu
// p.name ❌ Error: 'name' is private
// p.price ❌ Error: 'price' is protected
```

---

## 🔷 4. Interface + Constructor Params Kullanımı

```ts
interface IUser {
  username: string;
  email: string;
}

class User implements IUser {
  constructor(public username: string, public email: string) {}
}

const user = new User("tkmate", "tk@dev.com");
console.log(user.username); // ✅
```

---

## 🔷 5. Varsayılan Değerli Parametreler

```ts
class Config {
  constructor(public env: string = "development", public debug: boolean = true) {}
}

const defaultConfig = new Config();
const prodConfig = new Config("production", false);
```

---

## 🔷 6. Opsiyonel Parametreler (?)

```ts
class Student {
  constructor(public name: string, public grade?: number) {}

  printInfo() {
    console.log(`${this.name} - ${this.grade ?? "Not graded"}`);
  }
}
```

---

## 🔷 7. Tip Kombinasyonu (Union Types)

```ts
class Response {
  constructor(public status: "success" | "error", public data: any) {}
}

const res = new Response("success", { id: 1 });
```

---

## 🔷 8. Constructor İçinde Doğrulama

```ts
class Account {
  constructor(public balance: number) {
    if (balance < 0) throw new Error("Balance cannot be negative");
  }
}
```
