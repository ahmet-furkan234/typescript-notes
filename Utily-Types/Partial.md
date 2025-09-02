
## 🔹 `Partial<T>` Nedir?

TypeScript’in **Utility Types** (yardımcı tipler) arasında bulunur.  
Bir tipin **tüm property’lerini opsiyonel (`?`)** hale getirir.

👉 Yani elimizde bir interface varsa ve onu `Partial<T>` ile sararsak, o interface’in tüm alanlarını **isteğe bağlı** olarak kullanabiliriz.

---

## 🔹 Genel Kullanım

```ts
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```

Burada `keyof T` ile tipin tüm property’leri gezilir ve her birine `?` eklenir.  
Böylece hepsi opsiyonel olur.

---

## 🔹 Örnek

```ts
interface User {
  id: number;
  name: string;
  email: string;
}

let updateUser: Partial<User>;

updateUser = { name: "TkMatE" };          // sadece name olabilir
updateUser = { email: "test@test.com" };  // sadece email olabilir
updateUser = {};                          // boş obje bile geçerli
```

Normalde `User` tipinden bir obje oluştururken **tüm alanlar zorunlu**ydu.  
Ama `Partial<User>` sayesinde hepsi opsiyonel hale geldi.

---

## 🔹 Kullanım Senaryoları

### 1. Güncelleme İşlemleri (Update DTO)

Genelde bir **update** işlemi yapılırken her alanı göndermek zorunda olmayız.  
Sadece değişen alanları göndermek için `Partial` kullanılır.

```ts
function updateUserData(id: number, data: Partial<User>) {
  // data.id zorunlu değil, name ve email de opsiyonel
  console.log("Güncellenecek alanlar:", data);
}

updateUserData(1, { name: "Ahmet" });
updateUserData(2, { email: "abc@test.com" });
updateUserData(3, {}); // boş güncelleme de mümkün
```

---

### 2. Optional Config Yapıları

Bir fonksiyonun opsiyonel ayarlarını `Partial` ile kolayca tanımlayabiliriz.

```ts
interface Config {
  host: string;
  port: number;
  secure: boolean;
}

function connect(config: Partial<Config>) {
  console.log("Config:", config);
}

connect({ host: "localhost" }); // sadece host verdi
connect({ port: 3000, secure: true });
```

---

## 🔹 `Partial<T>` ile `?` Arasındaki Fark

- `?` kullanırsak sadece **tek bir property’yi opsiyonel** yaparız.
- `Partial<T>` ise **tüm property’leri opsiyonel** yapar.

```ts
interface A {
  x: number;
  y?: number;  // sadece y opsiyonel
}

type B = Partial<A>; 
// hem x hem y opsiyonel oldu
```

---

## 🔹 Gerçek Hayatta Örnek (API DTO)

```ts
interface CreateUserDto {
  username: string;
  password: string;
  email: string;
}

type UpdateUserDto = Partial<CreateUserDto>;
```

- `CreateUserDto` → kullanıcı oluştururken tüm alanlar zorunlu.
- `UpdateUserDto` → güncellemede sadece değişen alanları gönderebiliriz.

---

✅ Kısacası:  
`Partial<T>` → T’nin tüm property’lerini `optional` hale getirir.  
En çok **update DTO’ları** ve **opsiyonel config objeleri** için kullanılır.
