
TypeScript’te "object types", bir nesnenin sahip olması gereken:

- Özellik adlarını (property names)
- Ve her bir özelliğin veri türünü
açıkça tanımlamamızı sağlar.

---

## 🔹 1. Basit Object Type Tanımı

```ts
let kullanıcı: { ad: string; yaş: number } = {
  ad: "TkMatE",
  yaş: 25,
};
```

> Bu yapı der ki: `kullanıcı` nesnesi iki özelliğe sahip olmalı: `ad` (string) ve `yaş` (number)

---

## 🔹 2. Opsiyonel Özellikler (`?`)

Tüm nesne özellikleri zorunlu olmak zorunda değildir.

```ts
let kişi: { ad: string; yaş?: number } = {
  ad: "Ersin",
};
```

> Burada `yaş` verilmezse bile hata alınmaz çünkü `?` ile opsiyonel yapılmıştır.

---

## 🔹 3. Fazladan Özellik Kullanımı ❌

```ts
let hayvan: { tür: string } = {
  tür: "kedi",
  yaş: 3  // ❌ Error: yaş tanımlı değil
};
```

> TypeScript, fazladan özellikleri de yakalar. Eğer daha esnek bir yapı istersen index signature kullanman gerekir.

---

## 🔹 4. Index Signature (Dinamik property)

```ts
let ayarlar: { [key: string]: string } = {
  tema: "dark",
  dil: "tr",
  başka: "birşey"
};
```

> Bu, key’lerin string olduğu ve her key’in değerinin yine string olduğu dinamik bir yapı tanımlar.

---

## 🔹 5. Readonly Özellikler

Bir property’nin değiştirilemez olmasını istiyorsan `readonly` kullanılır:

```ts
let kullanıcı: { readonly id: number; ad: string } = {
  id: 1,
  ad: "TkMatE"
};

kullanıcı.id = 2; // ❌ Error: id değiştirilemez
```

---

## 🔹 6. Nested Object (İç içe nesneler)

```ts
let sipariş: {
  ürün: {
    ad: string;
    fiyat: number;
  };
  adet: number;
} = {
  ürün: {
    ad: "Kalem",
    fiyat: 10
  },
  adet: 3
};
```

---

## 🔹 7. Fonksiyon içeren object type

```ts
let logger: {
  mesaj: string;
  yaz(): void;
} = {
  mesaj: "Log kaydı",
  yaz() {
    console.log(this.mesaj);
  }
};
```

---

## 🔹 8. Type Alias ile Object Tanımı

Sürekli tekrar etmemek için `type` kullanabilirsin:

```ts
type Kullanıcı = {
  ad: string;
  yaş: number;
};

let k1: Kullanıcı = { ad: "Ahmet", yaş: 30 };
let k2: Kullanıcı = { ad: "Zeynep", yaş: 22 };
```

---

## 🔹 9. Object Types vs Interface (İpucu)

İleride `interface` konusunu işleyeceğiz ama burada minik bir karşılaştırma:

| Özellik                        | `type` ile object | `interface` |
| ------------------------------ | ----------------- | ----------- |
| Daha kısa tanım                | ✅                 | ✅           |
| Extend edilebilirlik           | ❌ sınırlı         | ✅ çok güçlü |
| Union & intersection kullanımı | ✅                 | ❌           |

---

## ✅ Özet

|Özellik|Açıklama|
|---|---|
|Object type tanımı|`{ ad: string; yaş: number }`|
|Opsiyonel property|`yaş?: number`|
|Sabit property|`readonly id: number`|
|Dinamik key|`{ [key: string]: string }`|
|Fonksiyon içeren|`{ yaz(): void }`|
