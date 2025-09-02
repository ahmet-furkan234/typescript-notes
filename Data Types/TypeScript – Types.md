
TypeScript, JavaScript’e **tip güvenliği (type safety)** ekler. Bu sayede değişkenlerin ve fonksiyonların hangi türde veri alıp döndürdüğü daha net olur. Kodlar daha sağlam ve hatasız yazılır.

---

## 🧩 Temel Türler (Primitive Types)

|Tür|Açıklama|Örnek|
|---|---|---|
|`string`|Metin veri türü|`let ad: string = "TkMatE"`|
|`number`|Sayılar (tamsayı & ondalıklı)|`let yaş: number = 25`|
|`boolean`|`true` veya `false`|`let aktifMi: boolean = true`|
|`null`|Boş veri|`let a: null = null`|
|`undefined`|Tanımsız değer|`let b: undefined = undefined`|
|`any`|Her tür veri alabilir (tip kontrolü yok)|`let karışık: any = "test"`|
|`unknown`|Türü bilinmiyor ama `any` kadar tehlikeli değil|`let x: unknown`|
|`void`|Genelde dönüş değeri olmayan fonksiyonlar|`function yaz(): void`|
|`never`|Asla bir değer dönmeyen durumlar|`function hata(): never`|

---

### 🔗 Örnek Kullanımlar:

```ts
let isim: string = "Ahmet";
let yaş: number = 30;
let aktif: boolean = true;
let notVerisi: any = 90;
let boşDeğer: null = null;
```

---

## 🧱 Referans Türler (Reference Types)

### 1. **Array (Dizi)**

```ts
let sayılar: number[] = [1, 2, 3];
let isimler: Array<string> = ["Ahmet", "Zeynep"];
```

---

### 2. **Tuple (Sabit tür sıralı dizi)**

```ts
let kullanıcı: [string, number] = ["TkMatE", 100];
```

---

### 3. **Enum**

```ts
enum Renk {
  Kırmızı,
  Yeşil,
  Mavi
}
let favori: Renk = Renk.Yeşil;
```

---

### 4. **Object (Nesne)**

```ts
let kişi: { isim: string; yaş: number } = {
  isim: "Ersin",
  yaş: 28
};
```

---

### 5. **Type Alias**

```ts
type Kullanıcı = {
  ad: string;
  yaş: number;
};

let tk: Kullanıcı = { ad: "TkMatE", yaş: 25 };
```

---

## 🧠 Özel Türler

### 1. **Union Types** (`|`)

```ts
let veri: string | number;
veri = "merhaba";
veri = 123;
```

---

### 2. **Literal Types**

```ts
let durum: "aktif" | "pasif";
durum = "aktif";
```

---

### 3. **Function Type**

```ts
function topla(x: number, y: number): number {
  return x + y;
}
```

---

### 4. **Optional (?)**

```ts
function selamla(ad?: string) {
  console.log(`Merhaba ${ad ?? "Ziyaretçi"}`);
}
```

---

### 5. **Readonly**

```ts
type Ürün = {
  readonly id: number;
  ad: string;
};

const urun: Ürün = { id: 1, ad: "Kalem" };
// urun.id = 2; ❌ HATA: id değiştirilemez
```

---

## 🔚 Sonuç:

- TypeScript'in gücü, tür sisteminden gelir.
    
- Bu türleri bilmek hata oranını ciddi azaltır.
    
- Kodlar daha **tahmin edilebilir**, **kolay okunabilir** ve **otomatize edilebilir** olur.
    

---

İstersen sıradaki konu olarak şunlara geçebiliriz:

1. **Type Inference (Tür Çıkarımı)**
    
2. **Advanced Types (Gelişmiş Türler: Intersection, Type Guards, keyof, infer vs.)**
    
3. **Interface vs Type farkı**
    

Hangisinden devam edelim TkMatE?