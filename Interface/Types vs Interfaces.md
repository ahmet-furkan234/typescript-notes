
Hem `type` hem `interface`:

✅ Yapıları tanımlamak için kullanılır  
✅ Nesne, fonksiyon, union, tuple vb. yapıların tiplerini belirleyebilir  
Ama bazı farkları vardır.

---

## 🎯 1. Temel Kullanım

**interface** genellikle nesne tipleri içindir:

```ts
interface Person {
  name: string;
  age: number;
}
```

**type** ile aynı şey yapılabilir:

```ts
type Person = {
  name: string;
  age: number;
};
```

> 🔹 Bu kullanımda fark yoktur.

---

## 🔄 2. Extend Etme (Kalıtım)

**interface** kalıtımı `extends` ile yapar:

```ts
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}
```

**type** ise `intersection (&)` ile birleştirme yapar:

```ts
type Animal = {
  name: string;
};

type Dog = Animal & {
  breed: string;
};
```

> 🔸 Her ikisi de kalıtımı destekler ama `interface` daha okunabilir ve genişletilebilir.

---

## 🧬 3. Fonksiyon Tipi Tanımlama

**type** burada daha yaygındır:

```ts
type Add = (a: number, b: number) => number;
```

**interface** ile de yapılabilir ama daha uzundur:

```ts
interface Add {
  (a: number, b: number): number;
}
```

> 🔸 Fonksiyon tipi tanımlamak için genelde `type` tercih edilir.

---

## 🧱 4. Union ve Tuple

Sadece `type` union veya tuple tanımlayabilir:

```ts
type Status = "success" | "error" | "loading"; // ✅
type Point = [number, number];                // ✅
```

```ts
interface Status = "success" | "error"; ❌ Geçersiz
interface Point = [number, number]; ❌ Geçersiz
```

> 🔺 Bu özellik sadece `type`’ta vardır.

---

## 🧩 5. Declaration Merging (Birleştirme)

**interface** birden fazla kez tanımlanabilir ve birleşir:

```ts
interface User {
  name: string;
}
interface User {
  age: number;
}

const u: User = {
  name: "TkMatE",
  age: 25
};
```

**type**'ta bu mümkün değildir:

```ts
type User = { name: string };
type User = { age: number }; ❌ Hata verir
```

> 🔸 Kütüphane geliştiricileri genellikle bu yüzden `interface` tercih eder.

---

## 📌 6. React Kullanımı Örneği

```tsx
// Genelde props için interface kullanılır:
interface Props {
  title: string;
  onClick(): void;
}

const Button = ({ title, onClick }: Props) => (
  <button onClick={onClick}>{title}</button>
);
```

---

## ✅ Ne Zaman Hangisini Kullanmalıyım?

|Durum|Önerilen|
|---|---|
|Nesne tipi tanımlama|`interface` 👍|
|Fonksiyon tipi|`type` 👍|
|Union / Tuple|`type` (tek seçenek)|
|İleride genişletilecek yapı|`interface` (çünkü birleşebilir)|
|API tipi tanımı (readonly, nullable vs.)|`type` daha esnek|

---

## 🧠 Kısa Notlar

|Özellik|`interface`|`type`|
|---|---|---|
|Kalıtım (extends)|✅|✅ (&)|
|Union / Tuple|❌|✅|
|Merge edilebilirlik|✅|❌|
|Fonksiyon tipi|⚠️ Daha zor|✅ Kolay|
|React props|✅ Yaygın|✅|

---

## 🎓 Sonuç

🔸 `interface`: Nesne ağırlıklı yapılar için, genişletilebilir ve okunabilir.  
🔸 `type`: Daha genel ve esnek, fonksiyon, union, tuple ve daha fazlası için ideal.

> En iyi yaklaşım: **interface ile başla**, yeterli değilse veya daha karmaşık şeyler gerekiyorsa `type`’a geç.

---

İstersen şimdi:

✅ `Classes vs Interfaces`  
✅ `Intersection Types`  
✅ `Discriminated Unions`  
✅ `Mapped Types`

gibi konularla devam edebiliriz. Hangisini seçelim TkMatE?