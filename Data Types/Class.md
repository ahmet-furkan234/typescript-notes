
## 🔹 1. Class Nedir?

Bir `class`, ortak özellikleri ve davranışları temsil eden bir **şablondur** (template). TypeScript’te `class`, JavaScript ES6 sınıflarının bir üst seviyesidir.

```ts
class Araba {
  marka: string;
  model: string;

  constructor(marka: string, model: string) {
    this.marka = marka;
    this.model = model;
  }

  bilgiVer() {
    console.log(`${this.marka} - ${this.model}`);
  }
}
```

---

## 🔹 2. Temel Yapı (Sınıfın Anatomisi)

```ts
class ClassAdı {
  // 🔸 Alanlar (Fields / Properties)
  // 🔸 Yapıcı Fonksiyon (Constructor)
  // 🔸 Metotlar (Methods)
}
```

Örnek:

```ts
class Kisi {
  isim: string;
  yas: number;

  constructor(isim: string, yas: number) {
    this.isim = isim;
    this.yas = yas;
  }

  selamla(): void {
    console.log(`Merhaba, benim adım ${this.isim}, ${this.yas} yaşındayım.`);
  }
}
```

---

## 🔹 3. Constructor (Yapıcı Fonksiyon)

Sınıf new ile oluşturulurken **ilk çalışan fonksiyondur**.

```ts
constructor(param1: Tip, param2: Tip) {
  // Değişken atamaları burada yapılır
}
```

---

## 🔹 4. Erişim Belirleyicileri (Access Modifiers)

| Erişim Belirleyici | Anlamı                                      |
| ------------------ | ------------------------------------------- |
| `public`           | Her yerden erişilebilir (varsayılandır)     |
| `private`          | Sadece sınıf içinde erişilebilir            |
| `protected`        | Sınıf içinde ve alt sınıflarda erişilebilir |
| `readonly`         | Sadece okunabilir, sonradan değiştirilemez  |

```ts
class Ogrenci {
  public ad: string;
  private not: number;
  protected seviye: string;
  readonly tcNo: string;

  constructor(ad: string, not: number, seviye: string, tcNo: string) {
    this.ad = ad;
    this.not = not;
    this.seviye = seviye;
    this.tcNo = tcNo;
  }

  public bilgiAl() {
    return `${this.ad} notu gizli, seviyesi ${this.seviye}`;
  }
}
```

---

## 🔹 5. Kısa Yol Constructor Tanımı

Alanları constructor içinde tanımlamak yerine **kısa şekilde** yazabilirsin:

```ts
class Kitap {
  constructor(
    public ad: string,
    public yazar: string,
    private sayfaSayisi: number
  ) {}
}
```

---

## 🔹 6. Metotlar (Methodlar)

Sınıf içinde tanımlanan fonksiyonlardır:

```ts
class HesapMakinesi {
  topla(a: number, b: number): number {
    return a + b;
  }
}
```

---

## 🔹 7. `this` Anahtarı

Sınıfın **kendi üyelerine** erişmek için kullanılır.

```ts
class Insan {
  isim: string;

  constructor(isim: string) {
    this.isim = isim;
  }

  yazdir() {
    console.log(this.isim);
  }
}
```

---

## 🔹 8. Inheritance (Kalıtım)

Bir sınıf başka bir sınıftan **miras alabilir**.

```ts
class Hayvan {
  sesCikar() {
    console.log("Ses çıkarıyor");
  }
}

class Kedi extends Hayvan {
  miyavla() {
    console.log("Miyav!");
  }
}

const kedim = new Kedi();
kedim.sesCikar(); // ✅
kedim.miyavla();  // ✅
```

---

## 🔹 9. Override (Üzerine Yazma)

Alt sınıf, üst sınıftaki metodu değiştirebilir.

```ts
class Arac {
  hareketEt() {
    console.log("Araç hareket ediyor");
  }
}

class Bisiklet extends Arac {
  override hareketEt() {
    console.log("Bisiklet pedal çeviriyor");
  }
}
```

---

## 🔹 10. `super` Anahtarı

Alt sınıfın, üst sınıfın **yapıcı fonksiyonu ya da metoduna** erişmesini sağlar.

```ts
class Ust {
  constructor(public isim: string) {}
}

class Alt extends Ust {
  constructor(isim: string, public seviye: number) {
    super(isim); // üst sınıf constructor’ı
  }
}
```

---

## 🔹 11. Statik Üyeler (`static`)

Sınıfın örneğine değil, sınıfın **kendisine ait** üyedir.

```ts
class Sayac {
  static adet: number = 0;

  constructor() {
    Sayac.adet++;
  }
}

new Sayac();
new Sayac();
console.log(Sayac.adet); // 2
```

---

## 🔹 12. Getters ve Setters

Sınıf özelliklerini **kontrollü şekilde okuma/yazma** sağlar.

```ts
class Urun {
  private _fiyat: number = 0;

  get fiyat() {
    return this._fiyat;
  }

  set fiyat(value: number) {
    if (value < 0) throw new Error("Negatif fiyat olamaz!");
    this._fiyat = value;
  }
}
```

---

## 🔹 13. Abstraction (Soyut Sınıf)

`abstract class` doğrudan kullanılamaz, ancak miras alınabilir.

```ts
abstract class Sekil {
  abstract alanHesapla(): number;
}

class Kare extends Sekil {
  constructor(public kenar: number) {
    super();
  }

  alanHesapla(): number {
    return this.kenar * this.kenar;
  }
}
```

---

## 🔹 14. Interface ile Kullanım

Sınıfın bir interface'i **uygulaması (implement etmesi)** gerekebilir.

```ts
interface Calisan {
  isim: string;
  calis(): void;
}

class Muhendis implements Calisan {
  constructor(public isim: string) {}
  calis(): void {
    console.log(`${this.isim} çalışıyor...`);
  }
}
```

---

## 🔚 Özet Tablo

|Özellik|Açıklama|
|---|---|
|`class`|Nesne şablonu oluşturur|
|`constructor`|Nesne oluşturulurken çalışan özel fonksiyon|
|`private`|Sadece sınıf içinden erişilebilir|
|`protected`|Sınıf ve alt sınıflardan erişilir|
|`readonly`|Sadece okunabilir, değiştirilemez|
|`extends`|Kalıtım sağlar|
|`super`|Üst sınıf constructor ya da metoduna erişim|
|`static`|Sınıf seviyesinde, örnek olmadan erişilebilir|
|`abstract`|Soyut sınıf, doğrudan kullanılamaz|
|`implements`|Interface kurallarını uygulamak için|
