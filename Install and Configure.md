
## ✅ 1. TypeScript Kurulumu

### 🔹 Global Kurulum (her yerden kullanılabilir)

```bash
npm install -g typescript
```

### 🔹 Yerel Kurulum (proje bazlı önerilir)

```bash
npm init -y                   # package.json oluştur
npm install --save-dev typescript
```

---

## ✅ 2. `tsc` Komutu ve İlk Derleme

### Basit `.ts` dosyası örneği:

📄 `hello.ts`

```ts
const name: string = "TkMatE";
console.log(`Merhaba, ${name}!`);
```

### Derleme:

```bash
npx tsc hello.ts
```

> `hello.js` dosyası oluşur, bu JS dosyası tarayıcı ya da Node ile çalıştırılabilir:

```bash
node hello.js
```

---

## ✅ 3. `tsconfig.json` Dosyası Oluşturma

> `tsconfig.json`, projenin TypeScript ayarlarını belirler.

### Oluşturmak için:

```bash
npx tsc --init
```

### Örnek Basit `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "ES6",              // Çıktı JavaScript versiyonu
    "module": "commonjs",         // Modül sistemi (Node için commonjs, web için ES6 önerilir)
    "outDir": "./dist",           // Derlenmiş dosyalar nereye gitsin?
    "rootDir": "./src",           // Kaynak TypeScript dosyaları nerede?
    "strict": true,               // Tüm sıkı tip kontrolleri aktif
    "esModuleInterop": true,      // `import` / `require` uyumu
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],        // Hangi dosyalar derlenecek?
  "exclude": ["node_modules"]     // Hangi klasörler hariç?
}
```

---

## ✅ 4. Proje Klasör Yapısı (Önerilen)

```text
project-root/
├── src/
│   └── index.ts
├── dist/
├── tsconfig.json
├── package.json
```

---

## ✅ 5. Derleme Komutu

```bash
npx tsc
```

> Tüm `src` içindeki `.ts` dosyaları derlenip `dist` klasörüne `.js` olarak gider.

---

## ✅ 6. Otomatik Derleme (Watch Mode)

```bash
npx tsc --watch
```

> Değişiklik yaptıkça anında `.js` dosyaları güncellenir.

---

## ✅ 7. VS Code Ayarları (isteğe bağlı)

- VS Code, TypeScript’i yerleşik destekler.
- `tsconfig.json` varsa otomatik tanır.
- `.ts` dosyası yazarken IntelliSense (otomatik tamamlama) sağlar.

---

## Bonus: `scripts` Tanımı (`package.json`)

```json
"scripts": {
  "build": "tsc",
  "watch": "tsc --watch",
  "start": "node dist/index.js"
}
```

```bash
npm run build    # derler
npm run watch    # değişiklikleri izler
npm run start    # çalıştırır
```

---

## ✅ Sonuç

| Aşama                                     | Durum |
| ----------------------------------------- | ----- |
| TypeScript yüklendi mi?                   | ✅     |
| İlk `.ts` dosyası yazıldı mı?             | ✅     |
| `tsconfig.json` ile proje yönetiliyor mu? | ✅     |
| Derleme ve çalıştırma yapılıyor mu?       | ✅     |
