
## 📌 1. Tanım

- **Statik Üyeler**: Bir sınıfın nesnesi üzerinden değil, sınıfın kendisi üzerinden erişilen özellikler ve metotlardır.
- `this` anahtar kelimesi, statik üyeler içinde **statik olmayanlara erişemez**.
- `static` üyeler genellikle yardımcı metotlar, sayaçlar veya paylaşılan veriler gibi durumlar için kullanılır.

---

## ✅ 2. Temel Örnek

```ts
class MathHelper {
  static PI = 3.14159;

  static square(x: number): number {
    return x * x;
  }
}

console.log(MathHelper.PI); // 3.14159
console.log(MathHelper.square(5)); // 25
```

- `MathHelper.PI` → sınıf örneği oluşturmadan doğrudan sınıf üzerinden erişildi.
- `MathHelper.square()` → statik fonksiyon olarak doğrudan kullanıldı.

---

## 🚫 3. Dikkat Edilmesi Gerekenler

```ts
class Counter {
  static count = 0;

  increment() {
    // Hatalı: statik alana this ile erişilemez
    // this.count++;
  }

  static increment() {
    this.count++;
  }
}
```

- Statik üyeler yalnızca sınıf adı veya `this` anahtar kelimesiyle, **yine statik bağlam** içinde erişilebilir.
- Sınıfın örnek metodundan `static` üyeye doğrudan erişilemez.

---

## 🔄 4. Statik Üyelerin Kullanım Senaryoları

|Senaryo|Açıklama|
|---|---|
|🔢 Sayaç (ID üretimi)|Her yeni nesne oluşturulduğunda artan ID|
|🛠 Yardımcı (utility) fonksiyonlar|`Math`, `Date`, `Logger` gibi sınıf örneği oluşturmadan işlev çağırmak|
|⚙ Paylaşılan ayarlar/config|Tüm örneklerde ortak kullanılan veriler|

---

## 🔁 5. Örnek: Otomatik ID Oluşturma

```ts
class User {
  private static nextId = 1;
  public id: number;

  constructor(public name: string) {
    this.id = User.nextId++;
  }
}

const u1 = new User("Ahmet");
const u2 = new User("Ayşe");

console.log(u1.id); // 1
console.log(u2.id); // 2
```

---

## 🧠 Özet

|Özellik|Açıklama|
|---|---|
|`static`|Üye sınıfa aittir, örneğe değil|
|Erişim|`ClassName.member` şeklindedir|
|Kullanım alanı|Yardımcı metotlar, sayaçlar, ortak yapılandırmalar|
|Erişim hatası|`this` ile statik üyeye erişmeye çalışmak|
