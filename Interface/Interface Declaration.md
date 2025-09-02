
# TypeScript Interface Declaration (Arayüz Bildirimi)

---

## 1. Interface Nedir?

`interface`, TypeScript'te **bir nesnenin yapısını tanımlayan, hangi özelliklere sahip olduğunu belirten** soyut bir şablondur.  
Bir `interface`, **tip güvenliğini sağlar** ve **kodda tutarlılığı korur**.

---

## 2. Neden Kullanılır?

- Nesnelerin sahip olması gereken alanları ve tipleri belirtmek için.
- Fonksiyon parametrelerinin, değişkenlerin veya sınıfların nasıl bir yapıya sahip olması gerektiğini tanımlamak için.
- Kodun daha okunabilir, bakımı kolay ve hata yapmaya karşı dirençli olmasını sağlamak için.

---

## 3. Basit Örnek

```ts
interface IUser {
  userName: string;
  email: string;
  age?: number;  // isteğe bağlı property
}

const user1: IUser = {
  userName: "tkmate",
  email: "tkmate@example.com"
};

const user2: IUser = {
  userName: "ahmet",
  email: "ahmet@example.com",
  age: 30
};
```

- `age?` soru işaretiyle **opsiyonel** hale getirilmiştir.

---

## 4. Interface’in Özellikleri

|Özellik|Açıklama|
|---|---|
|**Zorunlu alanlar**|Arayüzde belirtilen tiplerde alanlar|
|**Opsiyonel alanlar**|`?` işareti ile isteğe bağlı alanlar|
|**readonly alanlar**|Sadece okunabilir, değiştirilemez alanlar (`readonly`)|
|**Fonksiyon tipleri**|Arayüz içinde fonksiyon imzaları belirtilebilir|

---

## 5. Fonksiyon Tipi Olarak Kullanımı

```ts
interface ICalculate {
  (x: number, y: number): number;
}

const add: ICalculate = (a, b) => a + b;
```

---

## 6. Interface Extend (Kalıtım)

Arayüzler birbirinden türetilebilir:

```ts
interface IPerson {
  name: string;
}

interface IEmployee extends IPerson {
  salary: number;
}

const employee: IEmployee = {
  name: "TkMatE",
  salary: 5000
};
```

---

## 7. Class ile Interface Kullanımı

```ts
interface IUser {
  userName: string;
  email: string;
  getDisplayName(): string;
}

class User implements IUser {
  constructor(public userName: string, public email: string) {}

  getDisplayName() {
    return `${this.userName} <${this.email}>`;
  }
}
```

---

## 8. Interface ile Mongoose Entegrasyonu (Örnek)

```ts
import { Document } from "mongoose";

interface IUser extends Document {
  userName: string;
  email: string;
  phoneNumber: string;
  status: "aktif" | "pasif" | "engellendi";
}
```

---

# Özet

|Interface Ne İşe Yarar?|
|---|
|1. Nesne yapısını tanımlar ve tip güvenliği sağlar.|
|2. Kodun okunabilirliğini ve bakımını kolaylaştırır.|
|3. IDE desteği ile otomatik tamamlama sunar.|
|4. Karmaşık tip yapılarını (kalıtım, opsiyonel, readonly) destekler.|
