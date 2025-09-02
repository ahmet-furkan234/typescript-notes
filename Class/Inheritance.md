
- Kalıtım sayesinde bir sınıf, başka bir sınıfın özelliklerini ve metodlarını **miras alabilir (inherit)**.
- TypeScript’te `extends` anahtar kelimesiyle kullanılır.
- Alt sınıf (child/subclass), üst sınıfın (parent/base class) tüm `public` ve `protected` üyelerine erişebilir.

---

## 🔷 1. Temel Inheritance Örneği

```ts
class Person {
  constructor(public name: string, public age: number) {}

  greet(): void {
    console.log(`Hello, I am ${this.name}`);
  }
}

class Student extends Person {
  constructor(name: string, age: number, public grade: number) {
    super(name, age); // üst sınıf constructor’ı çağrılır
  }

  study(): void {
    console.log(`${this.name} is studying in grade ${this.grade}`);
  }
}

const student = new Student("TkMatE", 22, 12);
student.greet();  // Hello, I am TkMatE
student.study();  // TkMatE is studying in grade 12
```

---

## 🔷 2. Override (Metot Ezme)

Alt sınıf, üst sınıfın metodunu **kendi isteğine göre değiştirebilir** (override).

```ts
class Animal {
  makeSound(): void {
    console.log("Some generic sound");
  }
}

class Dog extends Animal {
  override makeSound(): void {
    console.log("Woof!");
  }
}

const dog = new Dog();
dog.makeSound(); // Woof!
```

> Not: TypeScript 4.3+ ile birlikte `override` yazmak önerilir.

---

## 🔷 3. `protected` Üyelerin Kullanımı

- `private`: sadece tanımlandığı sınıfta
- `protected`: hem o sınıf hem de ondan türeyen sınıflarda erişilebilir

```ts
class Vehicle {
  protected speed: number = 0;

  protected increaseSpeed(amount: number): void {
    this.speed += amount;
  }
}

class Car extends Vehicle {
  accelerate(): void {
    this.increaseSpeed(20);
    console.log(`Accelerated to ${this.speed} km/h`);
  }
}

const car = new Car();
car.accelerate();
// car.speed ❌ Hata: 'speed' is protected
```

---

## 🔷 4. Constructor Overriding

Alt sınıfta constructor varsa, üst sınıfın constructor’ı `super(...)` ile çağrılmak zorundadır.

```ts
class Employee {
  constructor(public name: string) {}
}

class Manager extends Employee {
  constructor(name: string, public department: string) {
    super(name); // Employee constructor çağrılır
  }
}
```

---

## 🔷 5. Çok Biçimlilik (Polymorphism)

```ts
class Shape {
  area(): number {
    return 0;
  }
}

class Square extends Shape {
  constructor(private side: number) {
    super();
  }

  override area(): number {
    return this.side * this.side;
  }
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  override area(): number {
    return Math.PI * this.radius ** 2;
  }
}

const shapes: Shape[] = [
  new Square(4),
  new Circle(3)
];

shapes.forEach(s => console.log("Alan:", s.area()));
```

---

## 🔷 6. Kalıtımla Gelen Özelliklerin Genişletilmesi

```ts
class User {
  constructor(public username: string) {}

  login(): void {
    console.log(`${this.username} logged in`);
  }
}

class AdminUser extends User {
  deleteUser(user: string) {
    console.log(`${this.username} deleted user: ${user}`);
  }
}
```

---

## 🔷 7. `instanceof` ile Tür Kontrolü

```ts
const u1 = new User("tk");
const a1 = new AdminUser("tkadmin");

console.log(u1 instanceof User);       // ✅ true
console.log(a1 instanceof AdminUser);  // ✅ true
console.log(a1 instanceof User);       // ✅ true, çünkü AdminUser -> User'dan türedi
```

---

## 🧪 Özelleştirme: BaseService → UserService

```ts
abstract class BaseService {
  constructor(public entityName: string) {}

  findAll() {
    console.log(`Listing all ${this.entityName}s`);
  }
}

class UserService extends BaseService {
  constructor() {
    super("User");
  }

  createUser(name: string) {
    console.log(`User ${name} created.`);
  }
}

const userService = new UserService();
userService.findAll();
userService.createUser("TkMatE");
```

---

## 🔚 Özet

|Özellik|Açıklama|
|---|---|
|`extends`|Kalıtım sağlar|
|`super()`|Üst sınıf constructor’ını çağırır|
|`override`|Metodu ezmek için|
|`protected`|Alt sınıflar erişebilir, dışarıdan erişilemez|
|`instanceof`|Tür kontrolü yapılabilir|
