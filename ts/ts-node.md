
`ts-node`, TypeScript dosyalarını **önce derlemeden, doğrudan çalıştırmanı** sağlar. Yani `.ts` dosyasını `.js`'e dönüştürmeden doğrudan Node.js içinde çalıştırır.

> `ts-node`, TypeScript için bir `Node.js` çalışma zamanı sağlar.

---

### ⚙️ Kurulum:

```bash
npm install -D ts-node typescript
```

Global kurulum istersen:

```bash
npm install -g ts-node typescript
```

---

### ▶️ Kullanım:

```bash
ts-node app.ts
```

Örnek:

```ts
// app.ts
const mesaj: string = "Merhaba ts-node!";
console.log(mesaj);
```

```bash
ts-node app.ts
# Output: Merhaba ts-node!
```

---

### ⚠️ Notlar:

- Derleme yapmadan TypeScript kodunu doğrudan çalıştırır.
- Geliştirme ortamında hızlı test için çok faydalıdır.
- Performans olarak üretim ortamına uygun değildir (ön derleme yapmadığı için).

---

### ✅ Ne Zaman Kullanılır?

- CLI araçları geliştirirken
- Küçük test scriptleri yazarken
- Hızlı TypeScript kodu denemeleri yaparken
