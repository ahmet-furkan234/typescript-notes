
## 🧠 1. Fonksiyon Tanımlama Şekilleri

### ✅ Normal Fonksiyon Tanımı

```ts
function greet(name: string): string {
  return "Hello, " + name;
}
```

- `name: string` → Parametre türü
- `: string` → Dönüş türü
- `return` → String döner

---

### ✅ Arrow Function (Ok Fonksiyonu)

```ts
const add = (a: number, b: number): number => {
  return a + b;
};
```

---

## 🧪 2. Fonksiyon Parametre Türleri

### 🎯 Zorunlu Parametre

```ts
function multiply(a: number, b: number): number {
  return a * b;
}
```

---

### ❓ Opsiyonel Parametre

```ts
function greet(name?: string): string {
  return name ? `Hello, ${name}` : "Hello!";
}
```

> `name?: string` → parametre verilmese bile hata vermez

---

### 🧾 Varsayılan Değerli Parametre

```ts
function greet(name: string = "Guest"): string {
  return `Hello, ${name}`;
}
```

---

## 🛠️ 3. Return Type (Dönüş Türü)

TypeScript’te dönüş tipi belirtebilirsin veya TypeScript bunu çıkarım (inference) yapabilir.

```ts
function toUpper(str: string) {
  return str.toUpperCase(); // inferred: string
}
```

Ama şunu da yazabilirsin:

```ts
function toUpper(str: string): string {
  return str.toUpperCase();
}
```

---

## 🧱 4. Fonksiyonların Türünü Tanımlama

TypeScript’te bir değişkene fonksiyon atarken **türünü tanımlayabilirsin**:

```ts
let log: (message: string) => void;

log = function(msg: string) {
  console.log(msg);
}
```

- `(message: string) => void` → Bu bir **function type**
- `void` → Dönüş değeri yok

---

## 🌀 5. Rest Parametreleri

Birden fazla argümanı dizi olarak almak istersen:

```ts
function sum(...numbers: number[]): number {
  return numbers.reduce((a, b) => a + b, 0);
}
```

---

## 🔄 6. Overloading (Aşırı Yükleme)

Bir fonksiyon farklı türlerde çalışabilir:

```ts
function combine(a: number, b: number): number;
function combine(a: string, b: string): string;
function combine(a: any, b: any): any {
  return a + b;
}
```

> İlk 2 satır **imza**, son satır **uygulama (implementation)** kısmıdır.

---

## 🧩 7. Callback Fonksiyonlar

Bir fonksiyon başka bir fonksiyonu parametre olarak alabilir:

```ts
function processInput(input: string, callback: (data: string) => void): void {
  callback(input.toUpperCase());
}
```

---

## 🔒 8. `void` vs `never` Dönüş Türü

|Dönüş Türü|Açıklama|
|---|---|
|`void`|Fonksiyon bir şey **döndürmüyor**|
|`never`|Fonksiyon **hiçbir zaman tamamlanmaz** (örnek: hata fırlatma)|

```ts
function throwError(): never {
  throw new Error("Something went wrong");
}
```

---

## 🎓 9. Fonksiyon Tipi Alias ile Tanımlama

```ts
type MathOperation = (a: number, b: number) => number;

const subtract: MathOperation = (a, b) => a - b;
```

---

## 💡 Özet

|Konu|Açıklama|
|---|---|
|Fonksiyon tanımı|`function`, `const = () => {}`|
|Parametre türleri|Zorunlu, opsiyonel, varsayılan, rest|
|Dönüş tipi|`string`, `void`, `never`, `any`, `unknown`|
|Fonksiyon tipi tanımı|`(a: number) => number`|
|Aşırı yükleme|Aynı isimde farklı parametre setiyle çalışma|
