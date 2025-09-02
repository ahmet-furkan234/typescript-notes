
**`tsc`**, TypeScript kodlarını (`.ts` dosyalarını) **JavaScript'e derleyen (transpile eden)** resmi TypeScript derleyicisidir.

> 📌 TypeScript → (tsc) → JavaScript

- Terminal veya komut satırından çalıştırılır
- Çalıştırıldığında `.ts` dosyasını `.js` dosyasına dönüştürür
- Derleme esnasında tip hataları kontrol edilir

---

### 🔹 2. `tsc` Nasıl Kurulur?

Proje genelinde kullanmak için:

```bash
npm install typescript --save-dev
```

Global (her yerden kullanılabilmesi için):

```bash
npm install -g typescript
```

Kurulumdan sonra şu komutla kontrol edebilirsin:

```bash
tsc -v
# Örnek çıktı: 5.4.2
```

---

### 🔹 3. Basit Kullanım

```bash
tsc app.ts
```

- `app.ts` dosyasını alır
- `app.js` dosyasına çevirir

Örnek:

```ts
// app.ts
let message: string = "Merhaba TypeScript!";
console.log(message);
```

```bash
tsc app.ts
# → app.js oluşturulur
```

---

### 🔹 4. `tsconfig.json` ile Derleme

`tsconfig.json` bir yapılandırma dosyasıdır. İçindeki ayarlarla `tsc` komutunun nasıl davranacağını belirler.

Kullanımı:

```bash
tsc --init     # tsconfig.json dosyası oluşturur
tsc            # tsconfig'e göre derleme yapar
```

---

### 🔹 5. İzleme Modu (Watch Mode)

Kod değiştikçe otomatik olarak yeniden derlemek için:

```bash
tsc -w
```

> Her değişiklikte `tsc` tekrar çalışır. Geliştirme sürecinde çok kullanışlıdır.

---

### 🔹 6. Birden Fazla Dosya Derleme

```bash
tsc dosya1.ts dosya2.ts
```

Veya `tsconfig.json` içine `include` verip sadece `tsc` yazarsın:

```json
{
  "include": ["src/**/*.ts"]
}
```

---

### 🔹 7. Common `tsc` Komutları

|Komut|Açıklama|
|---|---|
|`tsc`|tsconfig varsa ona göre derleme yapar|
|`tsc app.ts`|Tek bir dosyayı derler|
|`tsc -w`|İzleme (watch) modunda çalıştırır|
|`tsc --init`|tsconfig.json dosyası oluşturur|
|`tsc --build`|Projeyi yapılandırma dosyasına göre derler|
|`tsc --project ./configs/tsconfig.app.json`|Belirli bir tsconfig kullanır|

---

### 🔹 8. Örnek `tsc` Hataları

```ts
let x: number = "hello"; // ❌ Error: string assign to number
```

```bash
error TS2322: Type 'string' is not assignable to type 'number'.
```

`tsc` bu tür hataları _çalıştırmadan önce_ yakalar.

---

### 🔹 9. Otomatik Derleme İçin Ekstra

`tsc -w` dışında şunları da kullanabilirsin:

```bash
npx ts-node-dev src/index.ts
# Hem çalıştırır hem otomatik derler (ts-node ile)
```

---

### ✅ Özet

> `tsc`, TypeScript projelerinin **temel yapı taşıdır**. Derleme yapar, hataları kontrol eder ve JavaScript çıktısı oluşturur.

- Küçük projeler için direkt `tsc dosya.ts`
- Büyük projeler için `tsconfig.json + tsc`
- Geliştirme süreci için `tsc -w`
