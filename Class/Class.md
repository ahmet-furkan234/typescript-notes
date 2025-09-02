
Aşağıda sana temel bir giriş ve ardından ileri düzey `class` kullanım örnekleriyle açıklamalı bir anlatım sunacağım:

---

## 🔷 1. Temel TypeScript Class Kullanımı

```ts
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name}, and I am ${this.age} years old.`);
  }
}

const person1 = new Person("Ahmet", 25);
person1.greet();
```

### 📌 Açıklamalar:

- `name` ve `age` özellikleri tanımlandı.
- `constructor` ile sınıfın örneği oluşturulurken değer atandı.
- `greet()` bir metot (fonksiyon) olarak sınıf içerisinde tanımlandı.

---

## 🔷 2. Access Modifiers (Erişim Belirleyiciler)

TypeScript’te `public`, `private`, `protected`, `readonly` gibi belirleyiciler OOP’nin önemli bir parçasıdır.

```ts
class Car {
  private engine: string;
  readonly brand: string;

  constructor(brand: string, engine: string) {
    this.brand = brand;
    this.engine = engine;
  }

  startEngine(): void {
    console.log(`${this.brand} engine (${this.engine}) started.`);
  }
}

const car = new Car("BMW", "V8");
car.startEngine();

// car.engine // ❌ Error: 'engine' is private
// car.brand = "Mercedes" // ❌ Error: 'brand' is readonly
```

---

## 🔷 3. Inheritance (Kalıtım)

```ts
class Animal {
  constructor(public name: string) {}

  makeSound(): void {
    console.log("Some generic sound");
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log(`${this.name} says Woof!`);
  }
}

const dog = new Dog("Karabas");
dog.makeSound(); // Karabas says Woof!
```

---

## 🔷 4. Interface ile Class Kullanımı

```ts
interface IUser {
  username: string;
  email: string;
  login(): boolean;
}

class User implements IUser {
  constructor(public username: string, public email: string) {}

  login(): boolean {
    console.log(`${this.username} logged in with ${this.email}`);
    return true;
  }
}
```

---

## 🔷 5. Static Members (Sınıf Üzerinden Erişilen Özellikler)

```ts
class MathUtils {
  static PI = 3.14;

  static square(x: number): number {
    return x * x;
  }
}

console.log(MathUtils.PI); // 3.14
console.log(MathUtils.square(5)); // 25
```

---

## 🔷 6. Abstract Class

```ts
abstract class Shape {
  constructor(public color: string) {}

  abstract area(): number;

  describe(): void {
    console.log(`This is a shape with color ${this.color}`);
  }
}

class Circle extends Shape {
  constructor(color: string, public radius: number) {
    super(color);
  }

  area(): number {
    return Math.PI * this.radius ** 2;
  }
}

const circle = new Circle("red", 5);
circle.describe();
console.log(circle.area());
```

---

## 🔷 7. Getters ve Setters

```ts
class Product {
  private _price: number;

  constructor(price: number) {
    this._price = price;
  }

  get price(): number {
    return this._price;
  }

  set price(value: number) {
    if (value < 0) throw new Error("Price cannot be negative.");
    this._price = value;
  }
}

const p = new Product(100);
console.log(p.price); // 100
p.price = 150;        // setter
console.log(p.price); // 150
```

---

## 🔷 8. Dependency Injection ile Class Kullanımı (Yüksek Seviyeli)

```ts
interface ILogger {
  log(message: string): void;
}

class ConsoleLogger implements ILogger {
  log(message: string): void {
    console.log(`[LOG]: ${message}`);
  }
}

class App {
  constructor(private logger: ILogger) {}

  start(): void {
    this.logger.log("App started");
  }
}

const app = new App(new ConsoleLogger());
app.start();
```
