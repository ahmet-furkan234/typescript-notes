
**Enum**, sabit değerlerden oluşan özel bir türdür. Genellikle **durumları**, **rolleri**, **hataları** veya **seçenekleri** tanımlamak için kullanılır.

---

## ✅ 1. Basit `enum` Tanımı

```ts
enum Renk {
  Kirmizi,
  Yesil,
  Mavi
}

let r: Renk = Renk.Yesil;
console.log(r); // 👉 1
```

> Not: Varsayılan olarak `enum` üyeleri `0`'dan başlar ve sırayla artar.

---

## 🔢 2. Değer Atama (Manual Enum Values)

```ts
enum Renk {
  Kirmizi = 10,
  Yesil = 20,
  Mavi = 30
}

let r: Renk = Renk.Mavi;
console.log(r); // 👉 30
```

---

## 🔁 3. Enum’dan İsme Erişim (Reverse Mapping)

```ts
enum Renk {
  Kirmizi = 1,
  Yesil,
  Mavi
}

console.log(Renk[2]); // 👉 Yesil
```

> Sadece **numeric enum**'larda çift yönlü erişim vardır.

---

## 🆎 4. `String Enum`

```ts
enum Yön {
  Kuzey = "N",
  Guney = "S",
  Dogu = "E",
  Bati = "W"
}

let y: Yön = Yön.Kuzey;
console.log(y); // 👉 "N"
```

> String enum'lar **daha güvenlidir**, çünkü değerler değişmez.

---

## 🚫 5. Hatalı Enum Kullanımı

```ts
enum HataKodu {
  Basarili = 200,
  SunucuHatasi = 500
}

let hata: HataKodu = HataKodu[404]; // ❌ undefined
```

> Tanımlanmamış bir enum değeri kullanılmamalıdır.

---

## 🧩 6. Enum Kullanım Senaryoları

### Rol Tanımı:

```ts
enum Rol {
  Admin,
  Editor,
  Kullanici
}

function yetkileriYazdir(rol: Rol) {
  switch (rol) {
    case Rol.Admin:
      console.log("Tüm yetkilere sahip");
      break;
    case Rol.Editor:
      console.log("Düzenleme yetkisi var");
      break;
    case Rol.Kullanici:
      console.log("Sadece görüntüleyebilir");
      break;
  }
}
```

---

## 🔄 7. Enum'lar ile Object Literals Karşılaştırması

|Özellik|`enum`|`const object` literal|
|---|---|---|
|Tip desteği|Var|`typeof` ve `keyof` ile dolaylı|
|Derlenmiş çıktı|JavaScript koduna dönüşür|Sadece değer içerir|
|Performans|Biraz daha az|Daha hızlı|
|Reverse Mapping|Sadece sayısal enumlarda|Yok|

---

## 🧠 8. `const enum`

```ts
const enum Yon {
  Yukari,
  Asagi
}

let hareket: Yon = Yon.Yukari;
```

> Derleme sırasında enum sabitlerine doğrudan değer yazılır. Kod boyutunu azaltır.

```js
// çıktıda:
let hareket = 0;
```

> ⚠️ `const enum` kullanırken **reverse mapping yoktur** ve bazı `tsconfig` ayarlarında kullanılamaz (örnek: `isolatedModules: true`).

---

## 🧪 Enum ile Tip Kontrolü

```ts
function siparisDurumuKontrol(durum: SiparisDurumu) {
  if (durum === SiparisDurumu.Gonderildi) {
    console.log("Kargonuz yolda!");
  }
}

enum SiparisDurumu {
  Hazirlaniyor,
  Gonderildi,
  TeslimEdildi
}
```

---

## 📋 Özet

|Konu|Açıklama|
|---|---|
|`enum`|Sayısal değerli sabit küme|
|`string enum`|Daha güvenli, değişmeyen değerler|
|`const enum`|Derleme sırasında inlining yapar|
|`reverse mapping`|Sadece sayısal enum'larda vardır|
|Kullanım alanı|Roller, hatalar, durumlar, yönler|

---

Hazırsan TkMatE, sıradaki konuyu seçelim:

- 🔸 **Function Types**
    
- 🔸 **Union & Intersection Types**
    
- 🔸 **Interface vs Type**
    
- 🔸 **Type Narrowing**
    
- 🔸 **Type Guards**
    

Hangisiyle devam edelim?