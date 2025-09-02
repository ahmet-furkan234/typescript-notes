
`interface`, TypeScript’te bir **nesnenin şeklini (tipini)** tanımlar. Hangi alanların olması gerektiğini, veri tiplerini, varsa opsiyonellik durumlarını belirler.

> Yani bir `interface`, "bu nesne şunlara sahip olmalı" demektir.

---

## 📦 Temel Kullanım

```ts
interface Kullanici {
  ad: string;
  yas: number;
}

const kisi: Kullanici = {
  ad: "Ersin",
  yas: 30
};
```

Bu örnekte `kisi` değişkeni, `Kullanici` interface'inin kurallarına uymak **zorundadır**.

---

## 🔘 Opsiyonel Özellikler (`?`)

```ts
interface Kullanici {
  ad: string;
  yas?: number; // opsiyonel
}
```

> `yas` özelliği verilmese bile hata vermez. Kullanıcı sadece `ad` vermek zorundadır.

---

## ⛔ Readonly Özellikler

```ts
interface Ayarlar {
  readonly versiyon: string;
}

const appAyar: Ayarlar = {
  versiyon: "1.0.0"
};

appAyar.versiyon = "2.0.0"; // ❌ HATA: versiyon değiştirilemez!
```

> `readonly` ile tanımlanan alanlar sadece ilk atamada yazılabilir.

---

## 🔁 Method Tanımı

```ts
interface Hesaplayici {
  topla(a: number, b: number): number;
  carp(a: number, b: number): number;
}
```

> Interface içinde fonksiyon tanımı da yapılabilir. Sadece imzası (signature) gerekir.

---

## 🎭 Interface ile Class Kullanımı

```ts
interface Canli {
  isim: string;
  hareketEt(): void;
}

class Hayvan implements Canli {
  constructor(public isim: string) {}

  hareketEt() {
    console.log(`${this.isim} hareket ediyor`);
  }
}
```

> `implements` ile bir class, interface'i **uygulamak zorundadır**. Tüm alanları ve metodları eksiksiz içermelidir.

---

## 🔄 Interface Extend Etme (Inheritance)

```ts
interface Kisi {
  ad: string;
}

interface Calisan extends Kisi {
  maas: number;
}

const e1: Calisan = {
  ad: "Ahmet",
  maas: 7000
};
```

> Bir interface, başka bir interface'i miras alabilir.

---

## 🧩 Birden Fazla Interface Birleştirme (Intersection Types)

```ts
interface Kisi {
  ad: string;
}

interface Calisan {
  departman: string;
}

type CalisanKisi = Kisi & Calisan;

const ali: CalisanKisi = {
  ad: "Ali",
  departman: "IT"
};
```

> `type` ile `&` operatörü kullanılarak birden fazla interface birleştirilebilir.

---

## 📘 Index Signatures

```ts
interface Ayarlar {
  [key: string]: string | number;
}

const sistemAyar: Ayarlar = {
  tema: "dark",
  sürüm: 1.2,
  dil: "tr"
};
```

> Anahtar adlarının önceden bilinmediği durumlar için kullanılır.

---

## 🧠 `interface` vs `type` Arasındaki Farklar

|Özellik|`interface`|`type`|
|---|---|---|
|Extend (miras alma)|✔️ `extends`|✔️ `&` ile birleşir|
|Class ile kullanım|✔️ Uygun|✔️ Uygun|
|Fonksiyon tipi|❌ (dolaylı destek)|✔️ Daha kolay|
|Birleştirilebilirlik|✔️ `interface` ler birleşebilir|❌ `type` ler birleştirilemez|

---

## ✳️ Ne Zaman `interface`, Ne Zaman `type`?

- Nesne yapısı tanımı yapıyorsan → **interface**
    
- Union, intersection, fonksiyon tipi gibi daha esnek şeyler gerekiyorsa → **type**
    

---

## 🎯 Özet

- `interface` → nesne şablonu tanımlar.
    
- Class’lar ile uyumlu.
    
- Genişletilebilir, miras alabilir.
    
- Method, opsiyonel alan, readonly alan gibi özelliklere sahiptir.
    

---

İstersen sıradaki konuya `type aliases` veya `type` ile devam edebiliriz.  
Ya da interface’lerde `generic` kullanımı gibi daha ileri seviyeye geçebiliriz.

👉 Hangisiyle devam etmek istersin TkMatE?