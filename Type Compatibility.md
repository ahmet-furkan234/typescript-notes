
**Type Compatibility**, bir tipin başka bir tipe **atanabilir olup olmadığını** belirleyen kurallar bütünüdür.

> TypeScript’in tip sistemi **structural (yapısal)** tip sistemidir, yani bir nesnenin tipi adından çok **yapısına** bakılarak değerlendirilir.

---

## 🎯 Örnek 1: Basit Tip Uyumu

```ts
let x: number = 10;
let y: number = x; // ✅ uyumlu
```

Aynı türde olduğu için sorunsuz geçer.

---

## 🔗 Örnek 2: Object Type Uyumluluğu (Structural Typing)

```ts
type Kisi = { ad: string };
let kisi1 = { ad: "Ahmet", yas: 30 };

let kisi2: Kisi = kisi1; // ✅ kişi1, kişi2'ye atanabilir
```

> `kisi1`, `Kisi` tipinden daha fazla özellik içeriyor olsa bile, gerekli özellikleri (burada sadece `ad`) sağladığı için uyumludur.

---

## 🚫 Fazla Özellik Sorunu Yok

```ts
type A = { ad: string };
type B = { ad: string; yas: number };

let b: B = { ad: "Ali", yas: 25 };
let a: A = b; // ✅ B, A'ya atanabilir çünkü A'nın istediği her şeyi içeriyor
```

Ancak tersini yaparsan hata alırsın:

```ts
let a2: A = { ad: "Veli" };
let b2: B = a2; // ❌ Error: 'yas' eksik
```

---

## 🧠 Fonksiyon Uyumluluğu

### 1. Parametre Sayısı

```ts
let f1 = (a: number) => 0;
let f2 = (a: number, b: string) => 0;

f1 = f2; // ❌ f1 az parametre bekliyor, f2 fazla veriyor
f2 = f1; // ✅ f2, f1’in istediğini sağlayabilir
```

> Fazla parametreli fonksiyonu az parametreli olana atayamazsın.

---

### 2. Dönüş Tipi Uyumu

```ts
let fx = (): number => 10;
let fy = (): any => 20;

fx = fy; // ✅
fy = fx; // ✅
```

Ancak dönüş tipi uyumsuzsa:

```ts
let f3 = (): string => "merhaba";
let f4 = (): number => 42;

f3 = f4; // ❌ Tip uyumsuzluğu
```

---

## ✅ Class Uyumluluğu

```ts
class Hayvan {
  ad: string;
  constructor(ad: string) {
    this.ad = ad;
  }
}

class Kedi {
  ad: string;
  constructor(ad: string) {
    this.ad = ad;
  }
}

let h: Hayvan = new Kedi("Tekir"); // ✅ yapısal olarak uyumlu
```

> TypeScript isim değil **yapıya** bakar. Hem `Hayvan` hem `Kedi` sadece `ad: string` içerdiği için uyumludur.

---

## 🔀 Interface Uyumluluğu

```ts
interface Nokta2D {
  x: number;
  y: number;
}

interface Nokta3D {
  x: number;
  y: number;
  z: number;
}

let nokta3D: Nokta3D = { x: 1, y: 2, z: 3 };
let nokta2D: Nokta2D = nokta3D; // ✅
```

Ama tersini yapamazsın:

```ts
let nokta3D_2: Nokta3D = nokta2D; // ❌ z eksik
```

---

## 📌 Union ve Intersection Uyumları

```ts
type A = { a: number };
type B = { b: string };

type AB = A & B;
let obj: AB = { a: 1, b: "x" }; // ✅

let aOnly: A = obj; // ✅ AB, A’yı içeriyor
let bOnly: B = obj; // ✅ AB, B’yi de içeriyor
```

---

## 🔒 Type Guards ile Uyumlu Davranış

```ts
function isString(x: unknown): x is string {
  return typeof x === "string";
}

function kontrolEt(x: unknown) {
  if (isString(x)) {
    // Burada artık x: string olarak tip uyumlu
    console.log(x.toUpperCase());
  }
}
```

---

## 🧩 Generic Uyum Kuralları

```ts
function yazdir<T>(deger: T) {
  console.log(deger);
}

let f: <U>(deger: U) => void = yazdir; // ✅ Generic tipler uyumlu
```

---

## ❗️Type Compatibility Kurallarına Uymadığında Ne Olur?

1. Derleme hatası alırsın.
    
2. Kodun daha az güvenli hale gelir.
    
3. Tip çıkarımı (inference) ile karmaşa yaşanabilir.
    

---

## 🧠 Structural Typing vs Nominal Typing

TypeScript → **Structural**

> “Senin tipinin adı ne?” değil, **“içeriğinde neler var?”** diye bakar.

---

## 🎯 Özet

|Durum|Uyumluluk Durumu|
|---|---|
|Fazla özellik varsa|✅ Uygun|
|Eksik özellik varsa|❌ Uygun değil|
|Fonksiyon fazla parametre|❌ Uygun değil|
|Dönüş tipi uyuşuyorsa|✅ Uygun|
|Sınıf yapısı aynıysa|✅ Uygun|

---

## 🧪 İpucu

TypeScript'te bir tipi başka bir tipe atamadan önce tip uyumluluğunu test etmek için şu teknik kullanılabilir:

```ts
function assign<T>(val: T): T {
  return val;
}
```

Bu fonksiyonu kullanarak hangi tipin hangi tipe atanabildiğini test edebilirsin.

---

İstersen sıradaki konuyu `Type Assertion`, `Type Narrowing`, `Type Guards`, `Discriminated Unions`, ya da `Mapped Types` gibi ileri seviye type konularıyla sürdürebiliriz.

👉 Bir sonraki konun ne olsun TkMatE?