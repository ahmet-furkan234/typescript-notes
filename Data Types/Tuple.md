
**Tuple**, belirli **uzunlukta** ve **her elemanı belirli bir türde** olan bir dizidir. Dizilerden farkı: her elemanın tipi ve sırası önceden bellidir.

---

## ✅ 1. Temel Tuple Tanımı

```ts
let kisi: [string, number] = ["TkMatE", 25];
```

> Bu örnekte:

- 1. eleman: `string`
- 2. eleman: `number`

Her şey **sıralı ve sabit**.

---

## ❌ Hatalı Kullanım

```ts
let kisi: [string, number] = [25, "TkMatE"]; // ❌ Sıralama hatalı
let kisi2: [string, number] = ["TkMatE"];    // ❌ Eksik eleman
```

---

## 🧪 Tuple ile Fonksiyon Kullanımı

```ts
function konumAl(): [number, number] {
  return [40.7128, 74.0060]; // Enlem, boylam
}

let [enlem, boylam] = konumAl();
```

---

## 🧩 Tuple ile `readonly`

```ts
const koordinat: readonly [number, number] = [10, 20];
koordinat[0] = 99; // ❌ Hata: değiştirilemez
```

---

## 📌 Tuple’da Etiketli Kullanım (Yeni)

> TypeScript 4.0+ ile geldi.

```ts
let urun: [ad: string, fiyat: number] = ["Mouse", 250];
```

Bu sadece **dokümantasyon ve IDE desteği** içindir, çalışma zamanında etkisi yoktur.

---

## 🔄 Tuple + Array Fonksiyonları

```ts
let bilgi: [string, number] = ["TkMatE", 99];
console.log(bilgi[0].toUpperCase()); // TKMate
console.log(bilgi[1].toFixed(2));    // 99.00
```

---

## 🧠 Tuple ile Union Farkı

|Özellik|Tuple|Union Array|
|---|---|---|
|Eleman sayısı|Sabit|Belirsiz|
|Eleman tipi|Her biri farklı|Her biri belirli sınırlı türlerden|
|Kullanım amacı|Sıralı veri yapısı|Farklı tipte verileri aynı dizide tutmak|

---

## 🧱 Tuple Örneği: HTTP Cevabı

```ts
type HttpResponse = [status: number, body: string];

const cevap: HttpResponse = [200, "İşlem başarılı"];
```

---

## 📦 Tuple içeren Array

```ts
let skorlar: [string, number][] = [
  ["TkMatE", 100],
  ["Ahmet", 80],
  ["Ayşe", 90]
];
```

---

## 🚫 push() ile Sorun

```ts
let t: [string, number] = ["TkMatE", 5];
t.push("Yeni"); // ❗ Hata vermez ama beklenmeyen durum! (ES5 uyumu)
```

> Tuple'lar sabit yapı gibi görünse de push gibi metodlar hâlâ çalışabilir, bu yüzden dikkatli kullanılmalı.

---

## 📋 Özet

|Yapı|Açıklama|
|---|---|
|`[string, number]`|Sıralı ve sabit tipli 2 eleman|
|`readonly [...]`|Değiştirilemez yapı|
|`let [a, b] = tuple`|Destructuring ile ayrıştırma|
|`tuple.push(...)`|Teknik olarak izin verir ama önerilmez|
|`[type1, type2][]`|Tuple dizisi|
