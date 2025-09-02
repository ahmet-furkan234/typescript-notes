
`interface`, başka bir interface'i **`extends`** anahtar kelimesi ile devralabilir. Bu, bir interface'in üzerine yeni özellikler ekleyerek **yeniden kullanılabilir yapılar oluşturmanı sağlar**.

---

## 🧪 Temel Örnek:

```ts
interface Person {
  name: string;
  age: number;
}

interface Employee extends Person {
  employeeId: number;
}

const emp: Employee = {
  name: "TkMatE",
  age: 30,
  employeeId: 1234,
};
```

> ✅ `Employee`, `Person`’dan kalıtım aldı. Yani `Employee` hem `name` hem `age` hem de `employeeId` içeriyor.

---

## 🔄 Birden Fazla Interface Genişletme

```ts
interface Contact {
  email: string;
}

interface Address {
  city: string;
  country: string;
}

interface User extends Contact, Address {
  username: string;
}
```

```ts
const u: User = {
  email: "tk@example.com",
  city: "İstanbul",
  country: "Türkiye",
  username: "TkMatE"
};
```

> ✅ `User` üç ayrı interface’i birleştiriyor.

---

## 🧱 Uygulamalı Örnek (React benzeri props yapısı)

```ts
interface BaseProps {
  id: string;
}

interface ButtonProps extends BaseProps {
  label: string;
  onClick(): void;
}

const btn: ButtonProps = {
  id: "btn1",
  label: "Gönder",
  onClick: () => alert("Tıklandı")
};
```

> 🔔 Özellikle React’te `BaseProps`, `InputProps`, `ButtonProps` gibi interface'ler çok yaygındır.

---

## ❗ Interface Extend Edildiğinde Ne Olur?

- Önceki interface’in tüm alanları **zorunlu olarak miras alınır**
- Alanlar tekrar tanımlanamaz (tipi değiştirmek istersen `type` tercih edilir)
- Alanlar üzerine yazılamaz ama **opsiyonel alanlarla genişletilebilir**

---

## 🧠 Derin Not: Tip Güçlendirme

```ts
interface Animal {
  sound: string;
}

interface Dog extends Animal {
  breed: string;
}

const d: Dog = {
  sound: "Hav hav",
  breed: "Golden Retriever"
};
```

> ✅ Bu örnek, “bir `Dog` aynı zamanda `Animal`’dır” ifadesini tip düzeyinde güvence altına alır.

---

## ⚠️ interface ile type farkı burada da geçerli:

```ts
type A = { a: number };
type B = A & { b: number }; // ✅

interface C { c: number }
interface D extends C { d: number } // ✅
```

Ama:

```ts
interface E = A & { e: number }; // ❌ interface bunu yapamaz
```

---

## 🧩 interface extending interface — React’e Uygun Struct

```ts
interface HTMLProps {
  id?: string;
  className?: string;
}

interface InputProps extends HTMLProps {
  type: string;
  value: string;
  onChange: (val: string) => void;
}
```

> ✅ Genişletme sayesinde genel HTML props her bileşene ortak olarak verilebilir.

---

## ✅ Özet Tablo: `Extending Interfaces`

|Özellik|Açıklama|
|---|---|
|`extends` anahtar kelimesi|Kalıtım sağlar|
|Birden fazla interface devralma|Mümkün (`extends A, B`)|
|Alt interface üsttekini miras alır|✅|
|Özelliklerin tipi değiştirilemez|⚠️|
|React & OOP için çok kullanışlı|✅|
