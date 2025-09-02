
TypeScript'te equality, iki değerin **birbirine eşit olup olmadığını** kontrol etmek için kullanılır. 3 temel operatör vardır:

|Operatör|Anlamı|Tip kontrolü|Açıklama|
|---|---|---|---|
|`==`|Gevşek eşitlik|❌ Hayır|Tip dönüşümü yapar|
|`===`|Sıkı eşitlik|✅ Evet|Tip dönüşümü yapmaz|
|`Object.is()`|Hassas eşitlik|✅ Evet|`===`'e çok benzer ama `NaN` ve `-0` gibi özel durumları farklı değerlendirir|

---

## ✅ `==` (Loose Equality)

```ts
console.log(1 == "1");         // true → çünkü string "1" sayıya çevrilir
console.log(true == 1);        // true
console.log(null == undefined); // true
```

❗ **Uyarı**: Tip dönüşümü nedeniyle hatalı sonuçlara yol açabilir.

---

## ✅ `===` (Strict Equality – Tavsiye Edilen)

```ts
console.log(1 === "1");       // false → çünkü tipler farklı
console.log(true === 1);      // false
console.log(null === undefined); // false
```

> Her zaman **`===` ve `!==`** kullanmak önerilir çünkü tip güvenliğidir.

---

## ✅ `Object.is()` – İleri Seviye Eşitlik

`Object.is()` fonksiyonu, `===` gibidir ama bazı farklılıkları vardır:

```ts
console.log(Object.is(NaN, NaN));      // true
console.log(NaN === NaN);              // false

console.log(Object.is(+0, -0));        // false
console.log(+0 === -0);                // true
```

Yani:

- `Object.is()` daha doğru eşitlik kontrolü sağlar.
- Ancak çoğu durumda `===` yeterlidir.    

---

## 🎯 Type Narrowing ile Equality Kullanımı

```ts
function process(value: string | number) {
  if (typeof value === "string") {
    // TypeScript artık value'yu string olarak bilir
    console.log(value.toUpperCase());
  } else {
    // Geriye sadece number kalır
    console.log(value.toFixed(2));
  }
}
```

> TypeScript, `===` ile yapılan karşılaştırmalar sayesinde **tip daraltması** (type narrowing) uygular.

---

## ❗ `==` ile Tip Dönüşümlerine Örnek

```ts
console.log(false == 0);         // true
console.log("" == 0);            // true
console.log("" == false);        // true
```

Bu tür dönüşümler kafa karıştırıcıdır ve **hatalara açıktır**. TypeScript yazarken bunlardan kaçınmalısın.

---

## 🧠 Tipik Kullanım Alanları

- Koşullarda (`if`, `while`, ternary)
- Type narrowing (tip ayırımı)
- Custom type guard fonksiyonlarında
- Runtime veri kontrolünde (API’den gelen veriyi işleme gibi)

---

## 🔚 Sonuç

|Eşitlik Türü|Ne Zaman Kullanılır?|Güvenli mi?|
|---|---|---|
|`==`|Asla önerilmez|❌ Hayır|
|`===`|Her zaman önerilir|✅ Evet|
|`Object.is()`|Özel durumlar için|✅ Evet|
