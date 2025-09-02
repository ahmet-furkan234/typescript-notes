
> **Tanım:** Farklı sınıfların, aynı temel sınıftan türetilmiş olmalarına rağmen **ortak bir arayüzü (interface veya base class) kullanarak kendi davranışlarını gerçekleştirebilmesidir**.

### 🔑 Amaç:

- Ortak bir tip üzerinden işlem yaparken alt sınıfın **kendi özel davranışını** çalıştırmak.
- Kod tekrarını azaltmak, genişletilebilirliği artırmak.

---

## 🔹 1. Basit Bir Polymorphism Örneği

```ts
class Animal {
  makeSound(): void {
    console.log("Generic animal sound");
  }
}

class Dog extends Animal {
  override makeSound(): void {
    console.log("Woof!");
  }
}

class Cat extends Animal {
  override makeSound(): void {
    console.log("Meow!");
  }
}

const animals: Animal[] = [new Dog(), new Cat()];

animals.forEach(animal => animal.makeSound());
```

### 📌 Konsol Çıktısı:

```
Woof!
Meow!
```

> Burada `makeSound()` tüm nesneler için çağrılıyor, ancak her biri kendi sınıfının davranışını gösteriyor. Bu tam anlamıyla **runtime polymorphism**'dir.

---

## 🔹 2. Abstract Class ile Polymorphism

```ts
abstract class Shape {
  abstract area(): number;
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  override area(): number {
    return Math.PI * this.radius ** 2;
  }
}

class Square extends Shape {
  constructor(public side: number) {
    super();
  }

  override area(): number {
    return this.side * this.side;
  }
}

const shapes: Shape[] = [
  new Circle(5),
  new Square(4)
];

shapes.forEach(shape => console.log(shape.area()));
```

---

## 🔹 3. Interface ile Polymorphism

```ts
interface Logger {
  log(message: string): void;
}

class ConsoleLogger implements Logger {
  log(message: string): void {
    console.log("Console:", message);
  }
}

class FileLogger implements Logger {
  log(message: string): void {
    console.log("File:", message);
  }
}

function runApp(logger: Logger) {
  logger.log("Application started");
}

runApp(new ConsoleLogger()); // Console: Application started
runApp(new FileLogger());    // File: Application started
```

---

## 🔹 4. Polymorphic Method Parameters

```ts
function printAnimalSound(animal: Animal) {
  animal.makeSound();
}

printAnimalSound(new Dog()); // Woof!
printAnimalSound(new Cat()); // Meow!
```

> Polymorphism, **aynı fonksiyonla farklı nesneleri** işleyebilmeni sağlar.

---

## 🔹 5. Gerçek Dünya Senaryosu

### Kullanıcı rolleri örneği:

```ts
abstract class User {
  constructor(public username: string) {}

  abstract getPermissions(): string[];
}

class Admin extends User {
  override getPermissions(): string[] {
    return ["read", "write", "delete"];
  }
}

class Member extends User {
  override getPermissions(): string[] {
    return ["read"];
  }
}

function showPermissions(user: User) {
  console.log(`${user.username} permissions: ${user.getPermissions().join(", ")}`);
}

showPermissions(new Admin("adminUser"));   // adminUser permissions: read, write, delete
showPermissions(new Member("memberUser")); // memberUser permissions: read
```

---

## 🧠 Polymorphism Ne Sağlar?

|Avantajları|
|---|
|Kod tekrarını azaltır|
|Genişletilebilirliği artırır|
|Daha az if-else ile daha fazla esneklik|
|Dependency Injection ile uyumludur|
|Test yazımını kolaylaştırır|

---

## ❗ NOT: TypeScript’te “Method Overloading” sınırlıdır

TypeScript’te **method overloading** (aynı metodun farklı imzaları) sadece sınırlı desteklenir. Gerçek polymorphism genelde **alt sınıfın override ettiği metodlar** üzerinden çalışır.
