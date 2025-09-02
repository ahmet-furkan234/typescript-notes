
**"Truthy"** ve **"Falsy"**, bir değerin boolean bağlamda nasıl değerlendirildiğini belirtir.

> JavaScript/TypeScript'te **her değer**, `if` gibi koşullu ifadelerde **otomatik olarak boolean’a çevrilir.**  
> Bu çevirim sonucunda **"true" gibi davrananlara** `truthy`, **"false" gibi davrananlara** `falsy` denir.

---

## 🟥 Falsy Değerler

Aşağıdaki değerler **boolean bağlamda false** kabul edilir:

|Değer|Açıklama|
|---|---|
|`false`|Boolean false|
|`0`|Sayı olarak sıfır|
|`-0`|Negatif sıfır|
|`0n`|BigInt sıfır|
|`""`|Boş string|
|`null`|Null değeri|
|`undefined`|Tanımsız değer|
|`NaN`|Sayısal geçersiz değer|

```ts
if (0) {
  console.log("Bu çalışmaz.");
}

if ("") {
  console.log("Bu da çalışmaz.");
}
```

---

## ✅ Truthy Değerler

Yukarıdakiler dışında kalan tüm değerler **truthy** kabul edilir:

|Örnek Değerler|Açıklama|
|---|---|
|`"0"`|Boş olmayan string|
|`"false"`|String olduğu için truthy|
|`[]`|Boş dizi bile olsa truthy|
|`{}`|Boş nesne bile olsa truthy|
|`function() {}`|Fonksiyonlar|

```ts
if ("0") {
  console.log("Bu çalışır çünkü boş değil.");
}

if ([]) {
  console.log("Boş array bile truthy'dir.");
}
```

---

## 🧠 TypeScript ve Truthiness

TypeScript boolean'a otomatik dönüşümü anlar ama **bazı durumlarda uyarı verir**, örneğin:

```ts
function check(value: string | null) {
  if (value) {
    // value burada string olarak daraltılır
    console.log(value.toUpperCase());
  }
}
```

> TypeScript burada **`null` hariç string olduğunu** anlar. Bu duruma **truthiness narrowing** denir.

---

## 🔐 Örnek: Güvenli Kontroller

```ts
function printLength(s?: string) {
  if (s) {
    console.log(s.length); // s kesin string
  } else {
    console.log("Boş veya tanımsız.");
  }
}
```

---

## ❗ Kötü Kullanım

```ts
function isValid(user: string | number | null) {
  if (user) {
    // burada 0 da geçersiz sayılır!
    console.log("User var");
  }
}
```

Eğer `user = 0` ise bu **truthy kontrolü başarısız olur.**  
Bu yüzden **strict type check** önerilir:

```ts
if (user !== null && user !== undefined) {
  // daha güvenli
}
```

---

## ⛓️ Truthiness + Logical Operators

```ts
const username = inputName || "Varsayılan"; // inputName falsy ise "Varsayılan"
const isLoggedIn = user && user.token; // user varsa user.token alınır
```

---

## 🔄 Type Narrowing ile Truthiness

```ts
type Person = { name?: string };

function greet(p: Person) {
  if (p.name) {
    // name artık string (truthy olduğu için)
    console.log("Merhaba", p.name.toUpperCase());
  }
}
```

---

## 🧠 Özet

|Terim|Anlamı|
|---|---|
|`truthy`|boolean olarak true kabul edilen değer|
|`falsy`|boolean olarak false kabul edilen değer|
|Type Narrowing|Koşula göre tipin daraltılması|
|Riskli durum|`0`, `""`, `null`, `undefined` gibi değerler|

---

## 💡 Devam Önerisi

Truthiness konusunun ardından aşağıdakilerden birine geçebiliriz:

- 🔸 `Discriminated Union` (etiketli birleşimler)
    
- 🔸 `Literal Types`
    
- 🔸 `Optional Chaining` (`?.`)
    
- 🔸 `Nullish Coalescing` (`??`)
    
- 🔸 `Control Flow Analysis`
    

Hangisini istersin TkMatE?