
**Type Assertion**, TypeScript'e bir değerin belirli bir türe sahip olduğunu senin daha iyi bildiğini söylemenin bir yoludur.

TypeScript bazen bir değişkenin türünü doğru tahmin edemez. Bu gibi durumlarda sen açıkça “Bu değişken şu türde” diyebilirsin. Ama bu, **tip dönüşümü (type casting)** değildir! JavaScript'te çalışma zamanında hiçbir etkisi yoktur – **yalnızca derleyici düzeyinde bir ipucudur**.

---

## 🔤 Temel Sözdizimi

İki farklı kullanım biçimi vardır:

### 1. `as` sözdizimi (modern ve önerilen)

```ts
let veri: any = "Merhaba";
let uzunluk: number = (veri as string).length;
```

### 2. Açılı parantez `< >` (eski stil – JSX dışı yerlerde)

```ts
let veri: any = "Merhaba";
let uzunluk: number = (<string>veri).length;
```

> 🛑 JSX (React) kullanıyorsan sadece `as` sözdizimi kullanabilirsin. Çünkü `<string>` ifadesi HTML etiketi gibi algılanır.

---

## 📌 Neden Kullanılır?

1. **`any` veya `unknown` türündeki verileri daraltmak** için
2. **TypeScript’in anlayamadığı ama senin bildiğin durumlarda** tür belirtmek
3. DOM işlemlerinde (özellikle `document.querySelector`)
4. `null` kontrolü yapılamayan ama aslında emin olunan yerlerde

---

## 📚 Örnekler

### 1. `any` → `string` çevirip `.length` almak

```ts
let cevap: any = "Bu bir string";
let uzunluk = (cevap as string).length;
```

---

### 2. DOM Element tip belirtmesi

```ts
const inputEl = document.getElementById("email") as HTMLInputElement;
inputEl.value = "tkmate@example.com";
```

> Normalde `getElementById` dönüş tipi `HTMLElement | null` olur. Burada `HTMLInputElement` olduğunu belirttik.

---

### 3. `unknown` türünü kesinleştirme

```ts
let veri: unknown = "Merhaba dünya";

if (typeof veri === "string") {
  let büyükHarf = (veri as string).toUpperCase();
}
```

---

### 4. Nesneye özel tip atama

```ts
interface Kullanici {
  ad: string;
  yas: number;
}

let obj: any = {
  ad: "TkMatE",
  yas: 25
};

let kullanici = obj as Kullanici;
```

---

## 🚫 Dikkat: Güvenli Değilse Kullanma!

TypeScript sana sadece şunu der:

> “Tamam, madem sen bu değerin türünü biliyorsun, sana güveniyorum.”

Ama **yanlış tür belirtilirse** TypeScript hata vermez ama **çalışma zamanında uygulama çöker**.

```ts
let sayı: any = "bu bir yazı";
let kare = (sayı as number) * (sayı as number); // NaN ❌
```

---

## ✅ Güvenli Alternatifler

- `typeof` kontrolleri
- `instanceof`
- `user-defined type guards` (kullanıcı tanımlı tür kontrolleri)

---

## 🔎 Özet

|Amaç|Açıklama|
|---|---|
|`any` veya `unknown` daraltma|TypeScript’in emin olamadığı durumları sen bildirirsin|
|DOM işlemleri|`as HTMLInputElement` gibi tür bildirimi|
|Performans|Derleyici düzeyindedir, runtime etkisi yoktur|
|Risk|Yanlış kullanılırsa hata vermeden yanlış işler|
