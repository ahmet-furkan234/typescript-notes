
`unknown`, tıpkı `any` gibi **her tür değeri alabilir**, ancak onu kullanmadan önce **türünü kontrol etmen gerekir**.

> Yani: **`any` kadar esnek**, ama **çok daha güvenlidir**.

---

## 📦 Kullanımı

```ts
let veri: unknown;

veri = "merhaba";
veri = 42;
veri = true;
veri = { ad: "TkMatE" };
veri = [1, 2, 3];
```

Her türlü veri atanabilir ama doğrudan **kullanılamaz**:

```ts
let x: unknown = "merhaba";

// console.log(x.toUpperCase()); ❌ Hata: object is of type 'unknown'

if (typeof x === "string") {
  console.log(x.toUpperCase()); ✅
}
```

---

## 🎛️ `unknown` Kullanım Senaryoları

### 1. **Gelen veriyi önce kontrol etmek istiyorsan**

```ts
function mesajYaz(veri: unknown) {
  if (typeof veri === "string") {
    console.log(veri.toUpperCase());
  } else {
    console.log("Geçersiz tür");
  }
}
```

### 2. **Güvenli JSON parse işlemleri**

```ts
function parseJSON(str: string): unknown {
  return JSON.parse(str);
}

const gelenVeri = parseJSON('{"ad":"Ersin"}');

// gelenVeri.ad ❌ Olmaz
// typeof kontrolü yapılmalı!
```

---

## ❌ Direkt Kullanılamaz

```ts
let a: unknown = 5;

// let b = a + 3; ❌ HATA: unknown ile işlem yapılamaz

if (typeof a === "number") {
  let b = a + 3; ✅
}
```

> Bu sayede seni **hatalardan korur**.

---

## ✅ `any` vs `unknown` Karşılaştırması

|Özellik|`any`|`unknown`|
|---|---|---|
|Tip güvenliği|❌ Yok|✅ Var|
|Her tür atanır|✅ Evet|✅ Evet|
|Direkt kullanım|✅ Mümkün|❌ Önce kontrol edilmeli|
|Tavsiye|❌ Genelde kaçınmalısın|✅ Daha güvenli bir alternatif|

---

## 🛡️ Neden `unknown` Kullanmalısın?

- **Tip güvenliğini korur.**
    
- **Kodun bakımını kolaylaştırır.**
    
- **Yanlış kullanımı önler.**
    

---

## 🔧 Örnek: Gelişmiş Kullanım

```ts
function işlemYap(veri: unknown) {
  if (Array.isArray(veri)) {
    console.log("Dizi uzunluğu:", veri.length);
  } else if (typeof veri === "object" && veri !== null) {
    console.log("Object keys:", Object.keys(veri));
  } else {
    console.log("Tanımsız veya basit bir değer.");
  }
}
```

---

## 🧠 Hatırlatma: Tip Narrowing

```ts
if (typeof x === "string") {
  // x artık string gibi davranır
}
```

Bu işleme **Type Narrowing** denir. `unknown` ile çalışırken çok sık kullanılır.

---

## 🔚 Özet

|Konu|Açıklama|
|---|---|
|Tanım|Her türü alabilir ama güvenli kullanılır|
|Kullanım|JSON verileri, belirsiz dış kaynaklar|
|Güvenlik|`any`’ye göre çok daha güvenlidir|
|Kontrol şartı|Kullanılmadan önce `typeof`, `instanceof`|

---

İstersen sırada `never`, `void`, `function types`, `type guards`, ya da `union/intersection types` konularına geçebiliriz.

🔹 Hangisiyle devam edelim, TkMatE?