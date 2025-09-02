
TypeScript'te **getter** ve **setter** yöntemleri, bir sınıftaki özelliklere erişimi **kontrollü şekilde sağlamak veya değiştirmek** için kullanılır. Bu, "property overloading" olarak da bilinir ve özellikle veri doğrulama, özel iş mantıkları veya encapsulation (kapsülleme) için çok kullanışlıdır.

---

## 🧱 Söz Dizimi (Syntax)

```ts
class MyClass {
  private _property: string;

  get property(): string {
    // getter - değer okuma
    return this._property;
  }

  set property(value: string) {
    // setter - değer atama
    this._property = value;
  }
}
```

---

## 🧪 Basit Örnek

```ts
class Person {
  private _name: string = '';

  get name(): string {
    console.log("İsim okunuyor...");
    return this._name;
  }

  set name(value: string) {
    console.log("İsim ayarlanıyor...");
    if (value.length < 2) {
      throw new Error("İsim en az 2 karakter olmalı.");
    }
    this._name = value;
  }
}

const p = new Person();
p.name = "TkMatE";         // setter çalışır
console.log(p.name);       // getter çalışır
```

---

## 🎯 Özellikler

|Özellik|Açıklama|
|---|---|
|`get`|Özelliği okuma davranışını özelleştirir.|
|`set`|Özelliğe değer atandığında yapılacak işlemleri tanımlar.|
|private field|Genelde `get` ve `set` ile kullanılan alan `_` ile başlar (`_name`).|
|Kontrol Mek.|Set işlemi sırasında doğrulama, dönüştürme veya hata fırlatma yapılabilir.|

---

## 💡 Notlar

- `get` ve `set` aynı isimde tanımlanmalı ama farklı işleve sahiptir.
- Sadece `get` tanımlarsanız özellik sadece okunabilir olur.
- Getter ve Setter sayesinde dışarıdan erişim **kapsüllenmiş olur.**
- Getter/Setter olan bir alan, dışarıdan sanki **normal property gibi görünür.**

---

## 📌 TypeScript'te getter/setter kullanımı için `tsconfig.json`'da `target` değeri en az `ES5` olmalıdır.

---

## 🔐 Encapsulation ile Uyumlu Kullanım

```ts
class BankAccount {
  private _balance: number = 0;

  get balance(): number {
    return this._balance;
  }

  set balance(amount: number) {
    if (amount < 0) {
      throw new Error("Negatif bakiye olamaz.");
    }
    this._balance = amount;
  }
}

const account = new BankAccount();
account.balance = 1000; // setter
console.log(account.balance); // getter
```
