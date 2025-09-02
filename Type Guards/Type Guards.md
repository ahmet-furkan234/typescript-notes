
**Type Guard**, TypeScript’e bir değerin **hangi türde olduğunu çalışma zamanında anlamasını sağlayan özel bir ifadedir**. Böylece derleyici, belirli bloklar içinde daha **daraltılmış ve kesin** tiplerle işlem yapabilir.

---

## 🎯 Ne İşe Yarar?

- `union` veya `any` gibi **geniş türlerde** daha spesifik işlemler yapmayı sağlar
- TypeScript’in **otomatik type narrowing (tip daraltma)** özelliğinden yararlanır
- Tip güvenliği sağlar, `undefined is not a function` gibi hataları önler

---

## 🔍 Örnekler ile Type Guards Türleri

---

### ✅ 1. `typeof` ile Primitive Guard

```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(2));
  }
}
```

> 🔎 `typeof` yalnızca `string`, `number`, `boolean`, `symbol`, `bigint`, `function`, `undefined` için geçerlidir.

---

### ✅ 2. `in` Operatörü ile Property Guard

```ts
type Car = { drive: () => void };
type Boat = { sail: () => void };

function operate(vehicle: Car | Boat) {
  if ("drive" in vehicle) {
    vehicle.drive();
  } else {
    vehicle.sail();
  }
}
```

> 🔎 Bu yöntemde nesnenin **property adı kontrol edilir**, hangi tipe ait olduğu anlaşılır.

---

### ✅ 3. `instanceof` ile Sınıf Guard

```ts
class Dog {
  bark() {}
}
class Cat {
  meow() {}
}

function speak(animal: Dog | Cat) {
  if (animal instanceof Dog) {
    animal.bark();
  } else {
    animal.meow();
  }
}
```

> 🔎 Sadece **sınıf örneklerinde** kullanılabilir.

---

### ✅ 4. Özel (Custom) Type Guard Fonksiyonu

```ts
type Admin = { role: "admin"; permissions: string[] };
type User = { role: "user"; email: string };

function isAdmin(person: Admin | User): person is Admin {
  return person.role === "admin";
}

function accessPanel(person: Admin | User) {
  if (isAdmin(person)) {
    console.log(person.permissions); // Admin tipi olarak algılar
  } else {
    console.log(person.email); // User tipi
  }
}
```

> 🔎 Buradaki `person is Admin` ifadesi, **özel bir type guard tanımıdır**.

---

## 🧠 Neden `is` Kullanılır?

```ts
function isString(val: unknown): val is string {
  return typeof val === "string";
}
```

- Bu tanım, TypeScript'e **“Bu fonksiyon true dönerse, `val` artık `string` kabul edilir”** demek gibidir.

---

## 🧩 Type Guards + `keyof` + `in` Kombosu

```ts
type Shape = { kind: "circle"; radius: number } | { kind: "square"; side: number };

function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
  } else {
    return shape.side ** 2;
  }
}
```

> Bu örnek, TypeScript’in **discriminated union** (etiketli birleşim) özelliğiyle `kind` alanı üzerinden guard yapıyor.

---

## ❗️Not Edilmesi Gerekenler

- Type Guards sadece **runtime** seviyesinde geçerlidir.
- TypeScript, tipleri **otomatik olarak daraltmaz**; senin mantığınla anlar.
- Her zaman tüm `union` varyantlarını **ele alman** önerilir (`else`, `default`, `never` gibi).

---

## 📌 Özet Tablo

|Yöntem|Ne İçin Kullanılır|Sadece Şunlarla Geçerli|
|---|---|---|
|`typeof`|Primitive tipler (`string`, `number`, ...)|Primitive types|
|`in`|Property existence check|Object/Interface|
|`instanceof`|Sınıf örnekleri|Class|
|`custom guard`|Her türlü tip kontrolü|Her şeyle|

---

## 🔚 Sonuç

Type Guards, TypeScript’in JavaScript’ten daha **güvenli ve akıllı** olmasının temel sebeplerinden biridir. Karmaşık `union`, `any`, `unknown` tiplerde kod yazarken seni **run-time hatalardan kurtarır**.
