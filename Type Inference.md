
**Type Inference**, TypeScript’in sen açıkça bir tip belirtmesen bile değişkenin tipini **kendi başına tahmin etmesidir**.

> TypeScript: “Sen söylemesen de ben bu değerin türünü anladım!” der.

---

## 🧠 Basit Örnek

```ts
let mesaj = "Merhaba!";
```

Sen `mesaj` değişkeni için tip belirtmesen de, TypeScript `mesaj`'ın bir `string` olduğunu anlar:

```ts
// mesaj: string olarak algılanır
```

Artık `mesaj = 42` gibi bir şey yazarsan hata alırsın:

```ts
mesaj = 42; // ❌ HATA: number değeri string değişkene atanamaz.
```

---

## 🔍 Fonksiyonlarda Inference

### 1. Dönüş Tipi Inference

```ts
function topla(a: number, b: number) {
  return a + b;
}
```

> Burada `return` ifadesi bir `number` döndürdüğü için, TypeScript otomatik olarak dönüş tipini `number` olarak belirler.

```ts
// TypeScript çıkarımı:
// function topla(a: number, b: number): number
```

---

### 2. Parametrelerde Inference (YOK!)

```ts
function carp(a, b) {
  return a * b;
}
```

Bu fonksiyonda TypeScript `a` ve `b` için **herhangi bir çıkarım yapmaz** ve tipini `any` olarak kabul eder. Bu yüzden **her zaman parametrelerin tipini açıkça belirtmek önerilir**.

---

## 🔄 Const ve Let Farkı (Literal Inference)

```ts
let renk = "kırmızı"; // string olarak algılanır
const sabitRenk = "mavi"; // "mavi" (literal type) olarak algılanır
```

- `let` → `"kırmızı"` değeri verilir ama tipi `string` olur
    
- `const` → `"mavi"` değeri verilir ve literal olarak `"mavi"` tipi atanır
    

Bu davranış, union type veya string literal tanımlarken çok önemlidir.

---

## 🔗 Object Inference

```ts
let kisi = {
  ad: "Ahmet",
  yas: 25
};
```

Burada TypeScript şunu çıkarır:

```ts
{
  ad: string;
  yas: number;
}
```

Yani obje içindeki her property'nin tipi çıkarılır. Tip hatalarına karşı koruma sağlar:

```ts
kisi.yas = "otuz"; // ❌ string atanamaz!
```

---

## 📜 Dizi Tipi Inference

```ts
let sayilar = [1, 2, 3];
```

Bu durumda `sayilar` değişkeninin tipi:

```ts
number[]
```

Eğer karışık türde veri verirsen:

```ts
let karisik = [1, "iki", true]; 
// karisik: (string | number | boolean)[]
```

> TypeScript, elemanlara bakarak `union type` oluşturur.

---

## 🧪 İleri Seviye: Contextual Typing

Bazen çıkarım, **kontekstten** yapılır:

```ts
window.addEventListener("click", function(e) {
  console.log(e.clientX); // e, MouseEvent olarak çıkarılır
});
```

Sen `e` parametresine tip belirtmesen de, TypeScript `"click"` event'inden dolayı `e`'nin `MouseEvent` olduğunu anlar.

---

## 🧰 Tip Yardımı İçin `as const`

```ts
let renk = "kırmızı" as const;
```

Bu sayede TypeScript `renk`'in tipini `"kırmızı"` olarak kilitler. Genellikle sabit değerler (literal types) ile çalışırken kullanılır.

---

## 🔍 Özet

|Durum|TypeScript Ne Yapar?|
|---|---|
|`let x = 5`|`x: number` çıkarımı yapar|
|`let arr = [1, 2, 3]`|`number[]` tipi çıkarır|
|`const x = "selam"`|`"selam"` literal tipi çıkarır|
|`function f() { return 1; }`|`(): number` dönüş tipi çıkarır|
|`function(x) {}`|`x: any` olur (çünkü çıkarım yapılmaz)|
|`window.addEventListener`|Konteksten çıkarım yapılır (`e: MouseEvent`)|

---

## 🎯 Ne Zaman Açıkça Tip Belirtmeli?

- Fonksiyon parametrelerinde (her zaman önerilir)
    
- Karmaşık nesne yapılarında
    
- Kodun anlaşılmasını artırmak için
    
- API ile çalışırken (dış veri kaynakları)
    

---

İstersen sıradaki konuya `Type Assertion` (tip zorlama) veya `Literal Types` gibi inference ile bağlantılı konularla devam edebiliriz.

👉 Ne ile devam edelim TkMatE?