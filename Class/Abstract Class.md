
- `abstract class`, **soyut sınıftır**.
- Kendisi **doğrudan örneklenemez** (instance alınamaz).
- Genellikle diğer sınıflara bir **şablon** sunmak için kullanılır.
- İçinde hem:
    - **gerçekleştirilmiş (concrete)** metotlar olabilir
    - hem de **abstract (soyut)** metotlar olabilir (gövdesiz).

---

## 🔹 1. Temel Örnek

```ts
abstract class Animal {
  constructor(public name: string) {}

  abstract makeSound(): void; // soyut metot

  move(): void {
    console.log(`${this.name} is moving`);
  }
}

// const a = new Animal("some") // ❌ HATA: Soyut sınıflardan instance alınamaz

class Dog extends Animal {
  makeSound(): void {
    console.log(`${this.name} says: Woof!`);
  }
}

const dog = new Dog("Karabaş");
dog.makeSound(); // Karabaş says: Woof!
dog.move();      // Karabaş is moving
```

---

## 🔍 Açıklamalar:

- `abstract class Animal` → bir şablon sınıf
- `abstract makeSound()` → **alt sınıf bunu override etmek ZORUNDA**
- `move()` → tüm alt sınıflar kullanabilir, override etmek zorunda değil
- `Dog` sınıfı `Animal` sınıfından **kalıtım alıyor (extends)** ve `makeSound()` metodunu kendi içinde tanımlıyor

---

## 🔹 2. Birden Fazla Alt Sınıf Örneği

```ts
abstract class Shape {
  constructor(public color: string) {}

  abstract area(): number;

  describe(): void {
    console.log(`Shape with color: ${this.color}`);
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

class Square extends Shape {
  constructor(color: string, public side: number) {
    super(color);
  }

  area(): number {
    return this.side * this.side;
  }
}

const shapes: Shape[] = [
  new Circle("red", 5),
  new Square("blue", 4)
];

shapes.forEach(s => {
  s.describe();
  console.log("Area:", s.area());
});
```

### 🧠 Burada Ne Oldu?

- Hem `Circle` hem `Square`, `Shape` sınıfını genişletiyor.
- Her biri `area()` metodunu kendine özgü şekilde implement ediyor.
- `describe()` ortak fonksiyon olarak `abstract` sınıfta tanımlı.

---

## 🔹 3. Abstract Class vs Interface

|Özellik|`abstract class`|`interface`|
|---|---|---|
|Metot gövdesi olabilir mi?|✅ Evet|❌ Hayır|
|Constructor içerebilir mi?|✅ Evet|❌ Hayır|
|Çoklu kalıtım?|❌ Hayır|✅ Birden fazla interface|
|Alan (property) tanımı|✅ Evet (değer de verilebilir)|✅ Evet (sadece tip)|
|Amaç|Şablon/kalıp sağlamak|Davranış sözleşmesi tanımlamak|

🔸 Genellikle:

- `interface`: **ne yapılmalı** bilgisini verir
- `abstract class`: **nasıl yapılacağına dair** kısmı da içerir

---

## 🔹 4. Gelişmiş: Abstract + Dependency Injection

```ts
abstract class Logger {
  abstract log(message: string): void;
}

class ConsoleLogger extends Logger {
  log(message: string): void {
    console.log(`[LOG]: ${message}`);
  }
}

class App {
  constructor(private logger: Logger) {}

  start() {
    this.logger.log("App started.");
  }
}

const app = new App(new ConsoleLogger());
app.start();
```

---

## 🔐 Kullanım Senaryoları

- `Service` sınıflar için genel `BaseService`
- `Controller` yapılarında ortak iş mantıkları
- `Entity` sınıflarında ORM model kalıpları
- Testlerde soyut davranış tanımlama
