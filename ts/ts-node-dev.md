
`ts-node-dev`, `ts-node` + `nodemon` birleşimi gibi çalışan bir araçtır. Yani:

- `.ts` dosyalarını doğrudan çalıştırır
- Kodda değişiklik oldukça otomatik olarak uygulamayı **yeniden başlatır** (hot reload)

> TypeScript geliştirme sırasında sürekli elle yeniden çalıştırmaya gerek kalmaz. Geliştirici deneyimini ciddi şekilde iyileştirir.

---

### ⚙️ Kurulum:

```bash
npm install -D ts-node-dev typescript
```

---

### ▶️ Kullanım:

```bash
ts-node-dev src/app.ts
```

Veya `package.json` içinde:

```json
"scripts": {
  "dev": "ts-node-dev src/app.ts"
}
```

Ve çalıştırmak için:

```bash
npm run dev
```

---

### 🔁 Ne Yapar?

- Bellekte hızlı TypeScript derlemesi yapar
- Kod değişikliklerini izler (`watch`)
- Otomatik olarak sadece değişen modülü yeniden başlatır (fast restart)
- `ts-node`'dan daha hızlı ve verimlidir (çünkü modül önbelleği kullanır)

---

### 📝 Örnek Kod:

```ts
// app.ts
const now: Date = new Date();
console.log("Uygulama başladı:", now);
```

```bash
npm run dev
# Uygulama çalışır ve sen .ts dosyasını her kaydettiğinde otomatik olarak yeniden başlatılır.
```

---

### ✅ Ne Zaman Kullanılır?

- API veya CLI tabanlı projelerde geliştirme aşamasında
- Sürekli değişen back-end logic testleri yaparken
- Geliştirme sürecinde `fast refresh` ihtiyacı olan projelerde

---

### ⚠️ Notlar:

- Üretim ortamı için **kullanılmaz** (sadece development tool’dur)
- Bazı projelerde `--respawn` gibi ekstra parametreler gerekebilir

---

### 🚀 Hız Karşılaştırması:

| Araç          | Yeniden Derleme   | Otomatik Restart | Hız |
| ------------- | ----------------- | ---------------- | --- |
| `tsc`         | Manuel            | ❌                | 🐢  |
| `ts-node`     | Anında çalıştırır | ❌                | 🐢  |
| `ts-node-dev` | Anında + Watch    | ✅                | ⚡   |
