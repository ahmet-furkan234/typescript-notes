
Referans tipleri, **değerin kendisini değil bellekteki adresini** temsil eder. Yani bu türlerde yapılan değişiklikler, değişkenin kendisini değil, **referans verdiği veri yapısını** etkiler.

📌 **Temel Referans Tipleri:**

|Tip|Açıklama|
|---|---|
|`object`|Genel nesne tipi|
|`Array`|Dizi yapısı|
|`Tuple`|Sabit sayıda ve sıralı tipler|
|`Function`|Fonksiyonlar|
|`class` ve `interface`|Nesne modelleme|

---

## 🔹 1. `object` Tipi

```ts
let kisi: object = {
  ad: "TkMatE",
  yas: 25
};
```

> `object` tipi ile sadece nesne olduğunu belirtiyoruz, özellikler tiplenmiyor. Daha spesifik tanım için type/interface kullanılmalı.

```ts
let kisi2: { ad: string; yas: number } = {
  ad: "Ahmet",
  yas: 30
};
```

---

## 🔹 2. `Array` Tipi (Diziler)

### 🔸 Temel Kullanım

```ts
let sayilar: number[] = [1, 2, 3];
let isimler: string[] = ["Ali", "Veli"];
```

### 🔸 Generic Kullanımı

```ts
let sayilar: Array<number> = [10, 20, 30];
```

### 🔸 Çok Boyutlu Dizi

```ts
let tablo: number[][] = [
  [1, 2],
  [3, 4]
];
```

---

## 🔹 3. `Tuple` Tipi

> Tuple, **belirli sayıda öğe ve belirli tiplerde sıralı dizidir**.

```ts
let kullanıcı: [string, number] = ["Ersin", 30];
```

> İlk eleman string, ikinci eleman number olmalı. Sıralama önemlidir.

---

## 🔹 4. `Function` Tipi

### Fonksiyon tipi tanımı:

```ts
let topla: (a: number, b: number) => number;

topla = function (x, y) {
  return x + y;
};
```

> Parametre tipleri ve dönüş tipi (`=>`) açıkça belirtilmiştir.

---

## 🔹 5. `class` ve `interface`

### Class:

```ts
class Araba {
  marka: string;
  constructor(marka: string) {
    this.marka = marka;
  }
}
```

### Interface:

```ts
interface Kullanici {
  ad: string;
  email: string;
}

let k: Kullanici = {
  ad: "TkMatE",
  email: "tkmate@example.com"
};
```

---

## 🧠 Neden Referans Tipi?

Referans tipleri bellekte **stack yerine heap**'te tutulur. Bu nedenle şu davranış ortaya çıkar:

```ts
let a = { ad: "Ahmet" };
let b = a;

b.ad = "Mehmet";

console.log(a.ad); // "Mehmet"
```

> Çünkü `a` ve `b` aynı nesneye referans verir.

---

## ✅ Özet Tablosu

|Tip|Örnek|Açıklama|
|---|---|---|
|`object`|`{ ad: string }`|Serbest nesne tipi|
|`Array`|`number[]` veya `Array<string>`|Dizi tipi|
|`Tuple`|`[string, number]`|Sabit uzunlukta ve tipli dizi|
|`Function`|`(a: number) => string`|Fonksiyon tipi|
|`class`|`class Kullanici {}`|Yapı ve davranış modeli|
|`interface`|`interface Kullanici {}`|Sadece yapı tanımı (davranış yok)|

---

## 🚀 Sonraki Adım?

Aşağıdaki konulardan biriyle devam edebiliriz:

1. 🔸 **Function Types (Detaylı)**
    
2. 🔸 **Interface vs Type Alias**
    
3. 🔸 **Array Methods in TypeScript**
    
4. 🔸 **Union / Intersection Types**
    
5. 🔸 **Type Narrowing (Daraltma)**
    

Hangisini istersin TkMatE?