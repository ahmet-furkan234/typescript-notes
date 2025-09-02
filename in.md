
`in` operatörü, bir **özelliğin (property)** bir nesnede bulunup bulunmadığını kontrol eder.

```ts
"propertyName" in object
```

Eğer `"propertyName"` nesnede varsa, `true` döner.  
TypeScript bu durumda tip daraltması (type narrowing) yapabilir.

---

## ✅ Temel Örnek

```ts
type Person = { name: string; age: number };
type Animal = { species: string; sound: string };

function printInfo(entity: Person | Animal) {
  if ("name" in entity) {
    // entity artık kesin olarak Person
    console.log(`Name: ${entity.name}, Age: ${entity.age}`);
  } else {
    // entity artık kesin olarak Animal
    console.log(`Species: ${entity.species}, Sound: ${entity.sound}`);
  }
}
```

> `in` operatörü sayesinde TypeScript, fonksiyon içinde `entity` türünü **daraltır (narrowing)**.

---

## 🎯 Nesne Özelliklerini Kontrol Etme

```ts
const user = {
  id: 1,
  username: "tkmate"
};

console.log("id" in user); // true
console.log("email" in user); // false
```

---

## 🧪 `in` vs `typeof` vs `instanceof`

|Operatör|Kullanım Amacı|Örnek|
|---|---|---|
|`typeof`|Primitif türleri kontrol eder (`string`, `number`, vb)|`typeof x === "string"`|
|`instanceof`|Bir sınıfa ait olup olmadığını kontrol eder|`obj instanceof MyClass`|
|`in`|Nesnede bir özellik var mı diye kontrol eder|`"name" in obj`|

---

## 🧠 Not: `in`, sadece JS çalışma zamanında değil, TS derleme zamanında da çalışır

TypeScript bunu **type narrowing** için kullanır:

```ts
type Admin = { role: "admin"; permissions: string[] };
type Guest = { role: "guest" };

type User = Admin | Guest;

function getPermissions(user: User) {
  if ("permissions" in user) {
    // user artık Admin
    return user.permissions;
  }

  // user Guest
  return ["read-only"];
}
```

---

## ⚠️ Dikkat Edilecek Noktalar

- `in`, sadece **nesnelerde** çalışır.
    
- `in` kontrolü, sadece **property adının** varlığını kontrol eder. **Değerin tanımlı olup olmamasıyla ilgilenmez.**
    

```ts
const obj = { a: undefined };

console.log("a" in obj); // ✅ true
```

---

## ✅ Kapanış

`in` operatörü TypeScript'te:

- Type guard (tip koruyucu),
    
- Union type ayrıştırıcı,
    
- Özellik kontrolü,
    

olarak çok güçlü bir araçtır.  
Bundan sonra istersen:

- `Discriminated Union` konusuna geçebiliriz, çünkü `in` burada çok sık kullanılır.
    
- Ya da `typeof`, `instanceof`, `extends`, `literal types` gibi bağlamlara da ilerleyebiliriz.
    

👉 Hangisiyle devam edelim TkMatE?