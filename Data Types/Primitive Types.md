
İlkel türler, **JavaScript’in temel veri türleridir** ve TypeScript bu türleri statik olarak tanımlamamıza olanak sağlar. Aşağıda tüm temel türleri ve kullanımlarını görebilirsin:

---

### 1. `string`

**Açıklama:** Metinsel veri türüdür. Tek, çift veya ters tırnak (backtick) ile yazılır.

```ts
let isim: string = "TkMatE";
let mesaj: string = `Merhaba, ${isim}`;
```

---

### 2. `number`

**Açıklama:** Tam sayı, ondalık sayı, negatif/pozitif sayı olabilir.

```ts
let yaş: number = 30;
let sıcaklık: number = -12.5;
```

---

### 3. `boolean`

**Açıklama:** Mantıksal değer. `true` veya `false`.

```ts
let aktifMi: boolean = true;
let kullaniciGiris: boolean = false;
```

---

### 4. `null`

**Açıklama:** Bilinçli olarak boş bırakılan değer.

```ts
let veri: null = null;
```

---

### 5. `undefined`

**Açıklama:** Değeri tanımlanmamış değişkenler.

```ts
let açıklama: undefined = undefined;
```

> `undefined` genelde otomatik atanır ama elle de verilebilir. TypeScript’te `strictNullChecks` açık olduğunda dikkatli kullanılmalıdır.

---

### 6. `any`

**Açıklama:** Her türlü veri olabilir. **TypeScript’in tip kontrolünü devre dışı bırakır.**

```ts
let veri: any = "yazı";
veri = 100;
veri = true;
```

> 🔥 **Dikkat:** `any` kullanımı tip kontrolünü yok saydığı için önerilmez. Sadece geçici çözümler için tercih edilmelidir.

---

### 7. `unknown`

**Açıklama:** Türü bilinmeyen ama `any` kadar riskli olmayan tür. Kullanılmadan önce tür kontrolü gerekir.

```ts
let input: unknown = "deneme";

if (typeof input === "string") {
    console.log(input.toUpperCase());
}
```

> ✅ `unknown`, `any`'ye göre daha güvenlidir çünkü işlem yapılmadan önce tür kontrolü ister.

---

### 8. `void`

**Açıklama:** Fonksiyonlar dönüş değeri vermiyorsa kullanılır.

```ts
function logMesaj(): void {
    console.log("İşlem yapıldı.");
}
```

---

### 9. `never`

**Açıklama:** Hiçbir zaman bir değer döndürmez. Genellikle:

- Sonsuz döngü
- Hata fırlatma
- Ulaşılamaz kod gibi yerlerde kullanılır.

```ts
function hataVer(): never {
    throw new Error("Bir hata oluştu!");
}
```

---

## 🎯 Genel Örnek

```ts
let isim: string = "TkMatE";
let yaş: number = 27;
let aktif: boolean = true;
let bilinmeyen: unknown = 42;
let veri: any = "her şey olabilir";
let boşluk: null = null;
let eksik: undefined = undefined;

function selamla(): void {
    console.log("Merhaba!");
}
```

---

## 🧠 Notlar

- TypeScript'te her değişken tanımı tip belirterek yapılabilir.
- Yazmazsan, **type inference (tür çıkarımı)** ile otomatik tanır.
- `any` yerine `unknown` kullanmak genellikle daha güvenlidir.
- `null` ve `undefined` için dikkatli ol: `strictNullChecks` açıkken ek kurallar gerekir.
