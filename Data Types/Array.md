
TypeScript'te diziler, belirli bir türde elemanlar içerecek şekilde tanımlanabilir. Böylece dizideki tüm öğelerin tipi kontrol edilir.

---

## ✅ 1. Dizi Tanımlama Yöntemleri

### 🔹 Yöntem 1: `type[]` Söz Dizimi

```ts
let sayilar: number[] = [1, 2, 3, 4];
let kelimeler: string[] = ["merhaba", "dünya"];
```

### 🔹 Yöntem 2: `Array<type>` Generics Söz Dizimi

```ts
let sayilar: Array<number> = [1, 2, 3, 4];
let kelimeler: Array<string> = ["merhaba", "typescript"];
```

> İki yöntem de aynıdır. Tercih kişiseldir. Genellikle `type[]` daha kısa ve yaygındır.

---

## 🧪 2. Dizi Tipi ile Tip Hatalarını Engelleme

```ts
let isimler: string[] = ["TkMatE", "Ersin"];
isimler.push("Ahmet");     // ✅
isimler.push(123);         // ❌ Hata: 'number' tipi 'string' ile uyumsuz
```

---

## 🔄 3. Dizi ile Fonksiyon Kullanımı

```ts
function topla(sayilar: number[]): number {
  return sayilar.reduce((toplam, sayi) => toplam + sayi, 0);
}

console.log(topla([10, 20, 30])); // 60
```

---

## 🧩 4. Çok Boyutlu Dizi

```ts
let tablo: number[][] = [
  [1, 2, 3],
  [4, 5, 6]
];
```

> Burada her satır `number[]` olduğu için, `number[][]` tipi ile tanımlanır.

---

## 🟡 5. Union Type Dizi

Dizide farklı tiplerde veri tutulacaksa union tipi kullanılır:

```ts
let karisik: (string | number)[] = ["TkMatE", 42, "JS", 3];
```

---

## 🔐 6. Readonly Array (Salt Okunur Dizi)

Değerler değiştirilemesin istiyorsan:

```ts
let sabitler: readonly number[] = [3.14, 9.81];
sabitler.push(2.71); // ❌ Hata: push fonksiyonu yok
```

> `readonly` ile tanımlanmış bir dizide **eleman ekleyemez veya çıkaramazsın.**

---

## 📎 7. Tuple vs Array

|Özellik|Array|Tuple|
|---|---|---|
|Eleman Sayısı|Sınırsız|Belirli|
|Eleman Türleri|Aynı tür|Farklı tür|
|Kullanım Amacı|Liste gibi veriler|Sabit yapılar (id, ad, yaş vb.)|

Örnek:

```ts
let kisi: [string, number] = ["TkMatE", 30];
```

---

## 🔧 8. Tip Tanımlı Array Örneği

```ts
type Urun = {
  ad: string;
  fiyat: number;
};

let sepet: Urun[] = [
  { ad: "Klavye", fiyat: 200 },
  { ad: "Mouse", fiyat: 150 }
];
```

---

## 📋 Özet

|Tanım|Açıklama|
|---|---|
|`type[]`|Dizi tanımlamanın kısa yolu|
|`Array<type>`|Generics ile tanımlama|
|`readonly type[]`|Değiştirilemez dizi|
|`(type1|type2)[]`|
|`type[][]`|Çok boyutlu dizi|
|`type[]` + `reduce/map`|Fonksiyonlarla güçlü işlemler|

