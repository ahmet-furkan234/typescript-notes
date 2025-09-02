
`ts-loader`, TypeScript dosyalarını **Webpack aracılığıyla derlemek** için kullanılan bir **Webpack loader**'ıdır. Webpack yapılandırmasında `.ts` veya `.tsx` dosyalarını işler ve JavaScript’e dönüştürür.

> Yani `tsc` gibi derler ama Webpack ile entegredir. Bu sayede tek pakette derleme, modül birleştirme ve optimizasyon yapılır.

---

### ⚙️ Kurulum:

```bash
npm install -D typescript ts-loader webpack webpack-cli
```

> `webpack.config.js` içinde `ts-loader`'ı belirtmen gerekir.

---

### 📁 Örnek Webpack Yapılandırması:

```js
// webpack.config.js
const path = require('path');

module.exports = {
  entry: './src/index.ts',           // Başlangıç dosyası
  module: {
    rules: [
      {
        test: /\.ts$/,               // .ts uzantılı dosyaları hedef al
        use: 'ts-loader',
        exclude: /node_modules/,     // node_modules klasörünü hariç tut
      },
    ],
  },
  resolve: {
    extensions: ['.ts', '.js'],      // Hangi dosya uzantılarını çözümleyecek
  },
  output: {
    filename: 'bundle.js',           // Derlenmiş JS çıkışı
    path: path.resolve(__dirname, 'dist'),
  },
};
```

---

### 🗂️ Dosya Yapısı Örneği:

```
/src
 └── index.ts
webpack.config.js
tsconfig.json
package.json
```

---

### ▶️ Çalıştırma:

```bash
npx webpack
```

Veya `scripts` içine eklersen:

```json
"scripts": {
  "build": "webpack"
}
```

```bash
npm run build
```

---

### ✅ Ne Zaman Kullanılır?

- Webpack ile modül tabanlı front-end uygulamaları geliştirirken
- React, Vue, Angular gibi framework'lerle TypeScript kombinasyonlarında
- Üretim ortamı için optimize build işlemlerinde

---

### ⚠️ Notlar:

- `ts-loader`, `tsconfig.json` ayarlarını kullanır.
- Derleme + Bundle işlemini birlikte yapar.
- `babel-loader` + `@babel/preset-typescript` alternatifi de vardır.
