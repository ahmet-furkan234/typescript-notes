
`instanceof`, bir nesnenin belirli bir **class**'tan türetilip türetilmediğini kontrol eder.

```ts
nesne instanceof Constructor
```

> Bu ifade `true` dönerse, `nesne` belirtilen `Constructor`’dan (sınıftan) türemiştir demektir.

---

## 🔧 Temel Kullanımı

```ts
class Car {
  drive() {
    console.log("Driving");
  }
}

class Bike {
  pedal() {
    console.log("Pedaling");
  }
}

function useVehicle(vehicle: Car | Bike) {
  if (vehicle instanceof Car) {
    vehicle.drive(); // ✅ Car tipi olarak tanınır
  } else {
    vehicle.pedal(); // ✅ Bike tipi olarak tanınır
  }
}
```

TypeScript burada `vehicle` değişkenini `instanceof` sayesinde doğru tipe **daraltır**.

---

## 🧠 Neden `class` Lazım?

`instanceof`, sadece **constructor function** (yani `class`) üzerinden çalışır. `interface` veya `type` tanımlarında çalışmaz çünkü bunlar **runtime'da yoktur**.

**Yanlış:**

```ts
interface Animal {
  name: string;
}

let a: Animal = { name: "Leo" };

console.log(a instanceof Animal); // ❌ Error: 'Animal' only refers to a type, but is being used as a value
```

---

## 🧪 Örnek: Form Elemanı Tespiti

```ts
function handleElement(el: HTMLElement) {
  if (el instanceof HTMLInputElement) {
    console.log(el.value); // ✅ el artık HTMLInputElement tipi
  } else {
    console.log(el.innerText);
  }
}
```

---

## 🧬 Miras (Inheritance) ile Kullanım

```ts
class Shape {
  area() {
    return 0;
  }
}

class Rectangle extends Shape {
  constructor(public width: number, public height: number) {
    super();
  }

  area() {
    return this.width * this.height;
  }
}

function printArea(shape: Shape) {
  if (shape instanceof Rectangle) {
    console.log("Rectangle Area:", shape.area());
  } else {
    console.log("Generic Shape Area:", shape.area());
  }
}
```

> `instanceof`, miras alan sınıflarda hangi child sınıf olduğunu tanımamızı sağlar.

---

## ⚠️ Dikkat Edilmesi Gerekenler

|🧱 Özellik|Açıklama|
|---|---|
|✅ Yalnızca `class` ile çalışır|`type` ve `interface` ile çalışmaz|
|✅ Runtime kontrol sağlar|Yani JavaScript ortamında da çalışır|
|❌ Nesne farklı bir bağlamda oluşturulduysa (ör. iframe) `instanceof` başarısız olabilir||
|✅ `Type Guard` gibi davranır|TypeScript tipi daraltır|

---

## 🆚 `typeof` vs `instanceof`

|Özellik|`typeof`|`instanceof`|
|---|---|---|
|Kullanım Alanı|Primitive türler (`string`, `number`)|Nesne türleri, sınıflar|
|Ne döner?|`"string"`, `"number"` gibi string|`true` / `false`|
|Ne için kullanılır?|Basit tip kontrol|Class temelli nesne kontrolü|

---

## 🧠 İleri Seviye Tip Daraltma ile Kullanım

```ts
function isDate(value: unknown): value is Date {
  return value instanceof Date;
}

const input: unknown = new Date();

if (isDate(input)) {
  input.getFullYear(); // ✅ Artık input: Date
}
```

> Bu şekilde `instanceof`, **özel type guard fonksiyonları** yazmak için de kullanılabilir.

---

## ✅ Özet

- `instanceof`, runtime'da bir nesnenin **hangi class’a ait olduğunu** kontrol eder.
    
- TypeScript içinde **tip daraltma sağlar**.
    
- `type` veya `interface` tanımlarıyla çalışmaz.
    
- DOM, tarih, hata sınıfları gibi yapılarla kullanmak çok faydalıdır.
    

---

Bir sonraki adım olarak istersen şu konulara geçebiliriz:

- 🔹 `Discriminated Unions`
    
- 🔹 `typeof` operator (primitive tipi kontrolü)
    
- 🔹 `Custom Type Guards`
    
- 🔹 `Mapped Types`
    
- 🔹 `Conditional Types`
    

Hangisiyle devam etmek istersin TkMatE?