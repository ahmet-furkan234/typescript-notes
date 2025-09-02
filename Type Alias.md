
**Type Alias**, bir tipe takma ad vererek onu daha sonra kolayca kullanmamıza olanak tanır. Karmaşık tipleri tekrar tekrar yazmaktan kurtarır ve kodu okunur hale getirir.

---

### ✅ Temel Söz Dizimi

```ts
type MyString = string;
type Point = { x: number; y: number };
```

---

### 🧪 Kullanım Örneği:

```ts
type UserID = number;

let user1: UserID = 101;
let user2: UserID = 202;
```

---

## 🔸 2. Obje Tipleri İçin Alias

```ts
type User = {
  id: number;
  name: string;
  email?: string; // optional alan
};
```

```ts
const admin: User = {
  id: 1,
  name: "TkMatE"
};
```

---

## 🔸 3. Union ve Intersection ile Kullanımı

### 🔹 Union Tip:

```ts
type Status = "success" | "error" | "loading";

let currentStatus: Status = "success"; // ✅
```

### 🔹 Intersection Tip:

```ts
type Timestamps = {
  createdAt: Date;
  updatedAt: Date;
};

type Post = {
  id: number;
  title: string;
} & Timestamps;
```

---

## 🔸 4. Generic Type Alias

Type Alias, **generic** tanımıyla birlikte de kullanılabilir.

```ts
type ApiResponse<T> = {
  status: number;
  data: T;
};

const response: ApiResponse<string[]> = {
  status: 200,
  data: ["ok", "saved"]
};
```

---

## 🔸 5. Recursive Type Alias (Kendini Çağıran Yapılar)

```ts
type JSONValue = 
  | string 
  | number 
  | boolean 
  | null 
  | JSONValue[] 
  | { [key: string]: JSONValue };
```

Bu tarz yapılar JSON parser, AST vb. durumlarda oldukça işe yarar.

---

## 🔸 6. Fonksiyon Tipleri İçin Alias

```ts
type MathOperation = (x: number, y: number) => number;

const add: MathOperation = (a, b) => a + b;
const multiply: MathOperation = (a, b) => a * b;
```

---

## 🔸 7. Tuple ile Kullanım

```ts
type RGB = [number, number, number];

const red: RGB = [255, 0, 0];
```

---

## 🔸 8. Interface vs Type Alias

|Özellik|`type`|`interface`|
|---|---|---|
|Obje tanımı|✅|✅|
|Union/Intersection|✅|❌ (union tanımı yapamaz)|
|Extend edilebilirlik|Kısıtlı (ama `&` ile birleşebilir)|Daha doğal (interface extends)|
|Fonksiyon tanımı|✅|✅|
|Daha çok kullanıldığı yer|Generic, Function, Tuple, Union|Class, Public API, OOP yapıları|

> 📌 Genellikle `interface` **public API** için, `type` ise **daha genel ve güçlü kullanım** için tercih edilir.

---

## 🎯 Ne Zaman Type Alias Kullanmalı?

- Union veya intersection tipi oluşturuyorsan,
- Tuple veya fonksiyon tipi oluşturuyorsan,
- Karmaşık tipi tek satırda yeniden tanımlamak istiyorsan,
- Reusable (yeniden kullanılabilir) hale getirmek istiyorsan.

---

## 🔚 Özet

|Konsept|Açıklama|
|---|---|
|`type`|Tip tanımına takma ad vererek yeniden kullanılabilirlik sağlar|
|Union & Generic|Type ile birlikte mükemmel uyum sağlar (örneğin `type Api<T> = {...}`)|
|Fonksiyon, Tuple|Fonksiyon ve dizi tipleri için rahat kullanım sunar|
|interface vs type|Interface extend odaklıdır, type daha güçlü ve genel amaçlıdır|
