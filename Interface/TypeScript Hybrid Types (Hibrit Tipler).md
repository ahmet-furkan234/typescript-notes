
## 1. Hybrid Types Nedir?

**Hybrid types**, hem **fonksiyon** gibi çağrılabilen, hem de aynı zamanda **nesne gibi özelliklere ve metotlara sahip** yapılardır.

Yani hem fonksiyon **davranışı**, hem de nesne **özellikleri/metotları** aynı yapıda bir arada bulunur.

---

## 2. Neden Kullanılır?

JavaScript'te fonksiyonlar aslında **nesne** olduğu için, fonksiyonlara ek özellikler atayabiliriz.

TypeScript’te bu esnekliği tip sistemiyle tanımlamak için **interface** kullanılır.

---

## 3. Basit Örnek

```ts
interface Counter {
  (start: number): string; // Fonksiyon imzası
  interval: number;        // Özellik
  reset(): void;           // Metot
}

function getCounter(): Counter {
  let counter = <Counter>function (start: number) {
    return `Counter started at ${start}`;
  };
  counter.interval = 123;
  counter.reset = function () {
    console.log("Counter reset!");
  };
  return counter;
}

const c = getCounter();
console.log(c(10));    // "Counter started at 10"
console.log(c.interval); // 123
c.reset();             // "Counter reset!"
```

---

## 4. Açıklama

- `Counter` interface’i hem **fonksiyon tipi** hem de **nesne özelliklerini** belirtiyor.
- `getCounter()` fonksiyonu, bu hibrit tipte bir fonksiyon oluşturuyor.
- Fonksiyon olarak çağrılabiliyor (`c(10)`), aynı zamanda özelliklere (`c.interval`) ve metotlara (`c.reset()`) sahip.

---

## 5. Gerçek Dünya Kullanımı

- Timer objeleri (`setTimeout`, `setInterval`) veya
- Event emitter objeleri
- Fonksiyon nesneleri veya
- Jquery gibi callable obje tasarımlarında kullanılır.

---

## 6. Interface Örneği (Hibrit tip tanımı)

```ts
interface CallableCounter {
  (start: number): void;
  count: number;
  reset(): void;
}
```

---

## 7. Özet

|Hybrid Types Özelliği|Açıklama|
|---|---|
|Fonksiyon gibi çağrılabilir|`(start: number) => void`|
|Aynı zamanda nesne özellikleri|`count: number`, `reset(): void`|
|Fonksiyon nesneler oluşturulabilir|Dinamik ve esnek yapı sağlar|
