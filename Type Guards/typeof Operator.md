
`typeof` operatörü hem JavaScript’te hem TypeScript’te **primitive (ilkel) türleri** kontrol etmek için kullanılır. Özellikle union type içeren değişkenlerde, koşullara göre **tip daraltmak** için çok önemlidir.

---

## 📌 Söz Dizimi

```ts
typeof değer === "tip"
```

---

## 🧱 Kullanılabileceği Tipler

|`typeof` sonucu|Açıklama|
|---|---|
|`"string"`|Metin değerler|
|`"number"`|Sayısal değerler|
|`"boolean"`|Doğruluk değerleri|
|`"undefined"`|Tanımsız değerler|
|`"object"`|Nesneler, `null`|
|`"function"`|Fonksiyonlar|
|`"bigint"`|Büyük tamsayılar|
|`"symbol"`|Symbol tipleri|

---

## 🧪 Basit Örnek

```ts
function process(value: string | number) {
  if (typeof value === "string") {
    console.log("Metin uzunluğu:", value.length); // ✅ value artık string
  } else {
    console.log("Sayının karesi:", value * value); // ✅ value artık number
  }
}
```

---

## 🧠 Tip Daraltma (Type Narrowing)

`typeof`, TypeScript'in **union type** ifadelerde tipi otomatik daraltmasını sağlar.

```ts
type ID = string | number;

function printId(id: ID) {
  if (typeof id === "string") {
    console.log("ID büyük harfle:", id.toUpperCase()); // ✅ string metodları
  } else {
    console.log("ID karesi:", id * id); // ✅ number işlemleri
  }
}
```

---

## 🛑 `typeof` ve `null` Tuzağı

```ts
const a = null;
console.log(typeof a); // 🔴 "object" döner!
```

> Bu JavaScript’in eski bir bug’ıdır. `typeof null === "object"` ama `null` aslında primitive'dir.

---

## 🔧 Fonksiyon Tespiti

```ts
function maybeCall(fn: (() => void) | string) {
  if (typeof fn === "function") {
    fn(); // ✅ çağrılabilir
  } else {
    console.log("Metin:", fn);
  }
}
```

---

## 📦 `typeof` ile Tip Tanımlama (Type Queries)

> Bu, JavaScript’te değil sadece TypeScript’te geçerlidir.

```ts
const person = {
  name: "TkMatE",
  age: 25
};

type Person = typeof person;

const anotherPerson: Person = {
  name: "Ahmet",
  age: 30
};
```

### 📌 Açıklama:

- `typeof person`, `person` objesinin **tipini** otomatik alır.
- Bu özellikle büyük config dosyalarında veya reuse yapılacak yapıların tekrar tanımlanmasından kaçınmak için mükemmeldir.

---

## 🧠 `typeof` ile `keyof` Kombinasyonu

```ts
const user = {
  name: "Ersin",
  age: 20
};

type User = typeof user;
type UserKeys = keyof User; // "name" | "age"
```

---

## 🧪 Gelişmiş Kullanım: Dinamik Tip Alma

```ts
function clone<T>(source: T): T {
  return JSON.parse(JSON.stringify(source));
}

const settings = {
  darkMode: true,
  fontSize: 14
};

type SettingsType = typeof settings;

const defaultSettings: SettingsType = {
  darkMode: false,
  fontSize: 12
};
```

---

## ✅ `typeof` Özet

|Özellik|Açıklama|
|---|---|
|🧠 Tip daraltmak için kullanılır|`if (typeof x === "string")`|
|🔧 Primitive türler için uygundur|string, number, boolean, vs.|
|🔍 `type query` olarak da kullanılır|`type A = typeof value`|
|❌ Class ve interface için geçersiz|Bunun için `instanceof` gerekir|
|⚠️ `null` için `"object"` döner|Bu bir JS hatasıdır|

---

## 🔁 `typeof` vs `instanceof` Karşılaştırması

|Özellik|`typeof`|`instanceof`|
|---|---|---|
|Ne kontrol eder?|Primitive tipleri|Nesne / class tipleri|
|Dönen değer|`"string"`, `"number"` gibi|`true` veya `false`|
|Kullanım|`typeof x === "string"`|`x instanceof MyClass`|
|Type Narrowing|✅|✅|
