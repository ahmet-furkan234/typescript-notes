
**`never`**, bir fonksiyonun **asla sonlanmadığını** veya **hiçbir değer döndürmediğini** belirtir.

Yani:

- Sonsuz döngü
- Hata fırlatma
- Ulaşılamaz kodlar

---

## 🧪 Kullanım Senaryoları

### 1. ❗ Hata fırlatan fonksiyonlar

```ts
function hataVer(mesaj: string): never {
  throw new Error(mesaj);
}
```

➡️ Bu fonksiyon **hiçbir zaman başarıyla sonlanmaz**. Hata fırlatır, `return` etmez.

---

### 2. 🔁 Sonsuz döngüler

```ts
function sonsuz(): never {
  while (true) {
    console.log("Çalışıyor...");
  }
}
```

➡️ Bu fonksiyon **asla durmaz**, yani `return` etmez.

---

### 3. 🧭 Type Narrowing (Tip daraltma sırasında ulaşılmaz kod)

```ts
type Girdi = string | number;

function kontrolEt(x: Girdi) {
  if (typeof x === "string") {
    console.log("Bir string");
  } else if (typeof x === "number") {
    console.log("Bir sayı");
  } else {
    // x burada never olur çünkü tüm olasılıklar kontrol edildi
    const asla: never = x;
  }
}
```

---

## ⚠️ Neden `never` var?

`never`:

- **Kodun tüm olasılıklarını kapsayıp kapsamadığını kontrol etmek** için vardır.
- **Mantıksal hataları önler**.
- TS compiler’ı seni daha doğru kod yazmaya yönlendirir.

---

## 🔧 Gerçek Hayat Örneği

```ts
type Durum = "bekliyor" | "başarılı" | "hatalı";

function durumMesajı(durum: Durum): string {
  switch (durum) {
    case "bekliyor":
      return "İşlem bekliyor...";
    case "başarılı":
      return "İşlem tamamlandı!";
    case "hatalı":
      return "Bir hata oluştu.";
    default:
      // Buraya gelinmesi imkânsız!
      const kontrol: never = durum;
      return kontrol;
  }
}
```

✅ Eğer biri `"iptal edildi"` gibi yeni bir durum eklerse, TS hata verir ve seni uyarır.

---

## 📌 Farklar: `void` vs `never`

|Özellik|`void`|`never`|
|---|---|---|
|Değer döner mi?|❌ Hiçbir değer döndürmez ama sona erer|❌ Sona bile ermez (ya hata ya sonsuz döngü)|
|Kullanım Amacı|Fonksiyonun sonunda değer dönmüyorsa|Fonksiyonun **asla** bitmeyeceğini belirtir|
|Örnek|`function yaz(): void {}`|`function hata(): never { throw ... }`|

---

## 🔚 Özet

|Konu|Açıklama|
|---|---|
|Tanım|Hiçbir zaman sona ermeyen fonksiyonlar|
|Senaryolar|Hata fırlatma, sonsuz döngü, erişilemez kod|
|Avantaj|Tüm durumları kapsadığından emin olmak|
|TS katkısı|Kod doğruluğunu artırır, hata olasılığını azaltır|

---

İstersen sıradaki konumuz olarak `void`, `union types`, `type aliases`, `function return types`, ya da `type guards` konularından birini seçebilirsin.

🔹 Hangisiyle devam edelim TkMatE?