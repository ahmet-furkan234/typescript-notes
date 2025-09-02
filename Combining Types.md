
## 🔷 1. Union Types (`|`) – "Ya bu ya o"

### 📌 Tanım:

Bir değişkenin birden fazla farklı türden **birine** sahip olabileceğini ifade eder.

### ✅ Söz Dizimi:

```ts
let value: string | number;
```

### 🔍 Örnek:

```ts
function printId(id: number | string) {
  console.log("ID:", id);
}

printId(123);       // ✅
printId("ABC123");  // ✅
```

> 💡 Bu, **farklı senaryolar için esneklik sağlar**, ama her durumda **ortak olan özellikleri** kullanabilirsin.

---

## ⚠️ Union Kullanımında Dikkat

```ts
function getLength(input: string | number) {
  // return input.length; ❌ Hata! Çünkü number'da length yok.
  
  if (typeof input === "string") {
    return input.length; // ✅ Type Narrowing
  }

  return input.toString().length;
}
```

---

## 🔷 2. Intersection Types (`&`) – "Hem bu hem de o"

### 📌 Tanım:

Bir değişkenin **birden fazla türü aynı anda** taşımasını ifade eder. Yani tüm tiplerin birleşiminden oluşur.

### ✅ Söz Dizimi:

```ts
type Employee = {
  name: string;
  department: string;
};

type Admin = {
  name: string;
  permissions: string[];
};

type AdminEmployee = Employee & Admin;
```

### 🔍 Örnek:

```ts
const user: AdminEmployee = {
  name: "TkMatE",
  department: "IT",
  permissions: ["read", "write"]
};
```

> 🧠 Intersection Type, **birden fazla özellikli nesneler tanımlamak** için mükemmeldir.

---

## 🧪 Farkları (Union vs Intersection)

| Özellik        | Union                               | Intersection (`&`)                         |     |
| -------------- | ----------------------------------- | ------------------------------------------ | --- |
| Anlamı         | Herhangi biri                       | Hepsi bir arada                            |     |
| Kullanım Alanı | Fonksiyon parametrelerinde esneklik | Birden fazla özelliği birleştirme ihtiyacı |     |
| Tip Davranışı  | Ortak olanları kullanabilirsin      | Tüm alanlar kullanılabilir                 |     |

---

## 🔄 Union + Intersection – Birlikte Kullanım

```ts
type Dog = { kind: "dog"; bark: () => void };
type Cat = { kind: "cat"; meow: () => void };
type Animal = Dog | Cat;

function speak(animal: Animal) {
  if (animal.kind === "dog") {
    animal.bark(); // ✅
  } else {
    animal.meow(); // ✅
  }
}
```

> Literal type narrowing ile union türlerini kullanırken doğru metodu çağırmak mümkündür.

---

## 🧠 Derin Notlar

- Union tiplerde ortak olmayan alanlara direkt erişemezsin. **Type narrowing** gerekir.
- Intersection tiplerde tüm özellikler kullanılabilir. Ancak çakışan tiplerde dikkatli olmalısın.

### Çakışan Alanlar (Intersection’da)

```ts
type A = { val: string };
type B = { val: number };

type C = A & B; // ❌ HATA olur, çünkü `val` hem string hem number olamaz.
```

---

## 🔚 Özet

| Konsept            | Açıklama                                                     |
| ------------------ | ------------------------------------------------------------ |
| Union              |                                                              |
| Intersection (`&`) | Birden fazla tipi aynı anda taşıyan yeni bir tip oluşturur   |
| Kullanım Alanı     | Fonksiyon argümanları, yapı birleştirme, response types, vs. |
