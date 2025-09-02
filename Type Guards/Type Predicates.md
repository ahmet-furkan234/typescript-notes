
TypeScript’te **Type Predicate**, bir fonksiyonun dönüş tipini belirtirken kullanılır ve **bir değerin belirli bir tipe ait olduğunu garanti eder.**

```ts
function isString(value: unknown): value is string {
  return typeof value === "string";
}
```

🔍 Buradaki `value is string` ifadesi, **"eğer bu fonksiyon true dönerse, `value` bir string'dir"** anlamına gelir.

---

## 🧠 Neden Kullanılır?

Koşullara göre tip daraltmak istediğimizde normal `typeof`, `instanceof`, `in` yeterli olmayabilir. Kendi özel kontrolümüzü yapmak için type predicate tanımlarız.

---

## 🔧 Temel Kullanım

```ts
function isNumber(x: any): x is number {
  return typeof x === "number";
}

function doSomething(x: number | string) {
  if (isNumber(x)) {
    // Burada x: number
    console.log(x.toFixed(2));
  } else {
    // Burada x: string
    console.log(x.toUpperCase());
  }
}
```

### Açıklama:

- `isNumber(x): x is number` fonksiyonu bir **type guard** işlevi görür.
- TypeScript `if` bloğu içinde `x`'in **number olduğunu kesin olarak bilir.**

---

## 🎯 Örnek: Nesne Ayırt Etme

```ts
type Dog = { bark(): void };
type Cat = { meow(): void };

function isDog(animal: Dog | Cat): animal is Dog {
  return (animal as Dog).bark !== undefined;
}

function handleAnimal(a: Dog | Cat) {
  if (isDog(a)) {
    a.bark(); // Dog olduğu garanti
  } else {
    a.meow(); // Cat olduğu garanti
  }
}
```

---

## 💡 Daha Karmaşık Örnek

```ts
interface Admin {
  role: "admin";
  permissions: string[];
}

interface User {
  role: "user";
  name: string;
}

type Person = Admin | User;

function isAdmin(p: Person): p is Admin {
  return p.role === "admin";
}

function showInfo(p: Person) {
  if (isAdmin(p)) {
    console.log("Yetkiler:", p.permissions);
  } else {
    console.log("Adı:", p.name);
  }
}
```

> Bu örnekte Type Predicate ile `p`’nin `Admin` olup olmadığına karar veriyoruz.

---

## 🔄 Predicate Fonksiyonu Nerede Kullanılır?

- `if`, `else`, `ternary` yapılarında
- `filter`, `find`, `every` gibi dizi fonksiyonlarında

```ts
const mixed: (string | number)[] = [1, "a", 2, "b"];

function isString(val: string | number): val is string {
  return typeof val === "string";
}

const strings = mixed.filter(isString); // string[]
```

---

## ❗ `is` Zorunlu mu?

Evet. Bir **type predicate** tanımlamak için `is` kullanmak zorundasın. Aksi takdirde TypeScript **tipi daraltamaz**.

---

## 🧠 Özet

|Terim|Açıklama|
|---|---|
|`x is T`|Eğer fonksiyon true dönerse x'in T tipi olduğu garantilenir|
|Kullanım yeri|Type narrowing (tip daraltma) yapılacak fonksiyonların dönüş tipinde|
|Kullanım amacı|Karmaşık durumlarda TypeScript’in tipleri doğru anlamasını sağlamak|
|Alternatifler|`typeof`, `instanceof`, `in` (ama sınırlıdır)|
