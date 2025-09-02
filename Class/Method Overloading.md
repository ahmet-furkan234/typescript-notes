
**Method Overloading**, bir sınıf içinde aynı isme sahip ama farklı parametre sayısı veya türü olan birden fazla metodun tanımlanmasına olanak tanır.

> TypeScript derleyicisi JavaScript'e dönüştürüleceğinden, gerçek method overloading değil, _function signature overloading_ şeklinde çalışır. Gerçekte sadece tek bir method tanımı olur; diğerleri tanımlayıcıdır (declaration).

---

## 🔧 Temel Tanım

```ts
class Logger {
  log(message: string): void;
  log(code: number): void;
  log(param: string | number): void {
    if (typeof param === "string") {
      console.log("Message:", param);
    } else {
      console.log("Code:", param);
    }
  }
}

const logger = new Logger();
logger.log("Sunucu başlatıldı"); // Message: Sunucu başlatıldı
logger.log(404);                 // Code: 404
```

---

## 🧠 Açıklama

1. `log(message: string): void;` → **Sadece imza (signature)**, gövdesi yok.
2. `log(code: number): void;` → **İkinci bir imza**, farklı parametre tipiyle.
3. `log(param: string | number): void { ... }` → **Gerçek uygulama (implementation)**.

**TypeScript sadece bir uygulama (implementation) kabul eder. Diğerleri sadece tanım (declaration)** olarak kullanılır ve overload'lar derleyici tarafından kontrol edilir.

---

## 🧪 Örnek: Toplama İşlemi

```ts
class Calculator {
  add(a: number, b: number): number;
  add(a: string, b: string): string;
  add(a: any, b: any): any {
    return a + b;
  }
}

const calc = new Calculator();
console.log(calc.add(2, 3));         // 5
console.log(calc.add("Ahmet", "K")); // AhmetK
```

---

## 🚨 Kurallar

- Yalnızca bir tane **uygulama** (implementation) olabilir.
- **Tanımlar (signatures)**, uygulamadan önce olmalıdır.
- Parametre tiplerine göre çalışma koşulları içeride **`typeof`** gibi kontrollerle yapılır.

---

## 📌 Not: Neden Gerekli?

Method overloading, özellikle aynı işlevi gören ama farklı türlerle çalışan fonksiyonlar için okunabilirliği ve tip güvenliğini artırır.

Örneğin:

```ts
function readFile(path: string): string;
function readFile(buffer: Buffer): string;
// vs
function readFile(param: any): string { ... }
```

Bu şekilde bir API kullanıcısı, hangi türü kullanabileceğini daha net görür.

---

Hazırsan `Property Overloading (Getter-Setter)` gibi konularla devam edebiliriz ya da `Override` gibi inheritance tabanlı örneklerle ilerleyebiliriz. Hangisini istersin TkMatE?