
TypeScript’te 4 adet erişim belirleyici vardır:

|Belirleyici|Nereden Erişilir?|
|---|---|
|`public`|Her yerden (varsayılan erişim)|
|`private`|Sadece tanımlandığı sınıf içerisinden|
|`protected`|Tanımlandığı sınıftan ve ondan türeyen (inherit edilen) sınıflardan|
|`readonly`|Sadece okunabilir. Constructor’da veya tanımlandığı yerde değer atanabilir.|

---

## 🔹 1. `public` (Varsayılan)

Her yerden erişilebilir. Belirtilmezse bile `public` kabul edilir.

```ts
class Person {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const p = new Person("TkMatE");
console.log(p.name); // ✅ erişilebilir
```

---

## 🔹 2. `private`

Sadece **sınıfın içinden** erişilebilir.

```ts
class BankAccount {
  private balance: number;

  constructor(initial: number) {
    this.balance = initial;
  }

  deposit(amount: number) {
    this.balance += amount;
  }

  getBalance(): number {
    return this.balance;
  }
}

const account = new BankAccount(1000);
account.deposit(500);
console.log(account.getBalance()); // ✅ 1500
// console.log(account.balance);   // ❌ Hata: 'balance' is private
```

---

## 🔹 3. `protected`

- `private` gibidir ancak **alt sınıflar** da erişebilir.
    

```ts
class Animal {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }
}

class Dog extends Animal {
  bark(): void {
    console.log(`${this.name} says: Woof!`);
  }
}

const dog = new Dog("Karabas");
dog.bark(); // ✅ Karabas says: Woof!
// console.log(dog.name); // ❌ Hata: 'name' is protected
```

---

## 🔹 4. `readonly`

- Sadece **bir kez** atanabilir (tanımlama veya constructor içinde).
- Değiştirilemez.

```ts
class Config {
  readonly appName: string;

  constructor(name: string) {
    this.appName = name;
  }
}

const cfg = new Config("MyApp");
console.log(cfg.appName); // ✅ MyApp
// cfg.appName = "OtherApp"; // ❌ Hata: 'appName' is readonly
```

---

## 🧠 Erişim Belirleyiciler Constructor'da Nasıl Kullanılır?

```ts
class Product {
  constructor(
    public readonly id: number,
    private name: string,
    protected price: number
  ) {}

  print(): void {
    console.log(`${this.name} - $${this.price}`);
  }
}

class SaleProduct extends Product {
  applyDiscount(discount: number) {
    this.price -= discount;
  }
}
```

---

## 🧪 Özet Karşılaştırma

|Özellik|`public`|`private`|`protected`|`readonly`|
|---|---|---|---|---|
|Dışarıdan erişilebilir|✅|❌|❌|✅ (okunur)|
|Alt sınıftan erişim|✅|❌|✅|✅ (okunur)|
|Yazılabilir mi?|✅|✅|✅|❌ (sadece constructor’da)|
