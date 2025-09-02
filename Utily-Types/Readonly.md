
## 🔹 `Readonly<T>` Nedir?

`Readonly<T>`, bir tipin **tüm property’lerini sadece okunabilir (immutable)** hale getirir.  
Yani oluşturduktan sonra property değerlerini değiştiremezsin.

---

## 🔹 Genel Kullanım

```ts
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};
```

- Burada `readonly` ile her property’ye salt-okunur özelliği kazandırılır.
- `keyof T` → T’nin tüm property’leri üzerinde gezinir.

---

## 🔹 Örnek

```ts
interface User {
  id: number;
  name: string;
  email: string;
}

const user: Readonly<User> = {
  id: 1,
  name: "TkMatE",
  email: "tkmate@test.com"
};

user.name = "Ahmet"; 
// ❌ Error: Cannot assign to 'name' because it is a read-only property
```

---

## 🔹 Kullanım Senaryoları

### 1. Objelerin Değişmezliğini Sağlamak (Immutable Objects)

Özellikle büyük projelerde **state management** veya **config ayarları** değişmesin istenir.

```ts
interface Config {
  host: string;
  port: number;
  secure: boolean;
}

const config: Readonly<Config> = {
  host: "localhost",
  port: 3000,
  secure: true
};

// config.port = 4000; ❌ değiştirilemez
```

---

### 2. Fonksiyon Parametrelerini Koruma

Fonksiyon içinde yanlışlıkla parametre değiştirilmesini engelleyebilirsin.

```ts
interface Todo {
  title: string;
  completed: boolean;
}

function printTodo(todo: Readonly<Todo>) {
  console.log(todo.title, todo.completed);
  // todo.completed = true; ❌ değiştirilemez
}

printTodo({ title: "Learn TS", completed: false });
```

---

### 3. `const` ile Farkı

- `const` → değişkenin referansını değiştirmeyi engeller.
- `Readonly<T>` → objenin içindeki property’lerin değerini değiştirmeyi engeller.

```ts
const user = { id: 1, name: "TkMatE" } as const;

// burada hem objeyi hem property’leri sabit yapar
// Readonly<T> ise sadece property’leri sabitler
```

---

✅ Özet:

- `Readonly<T>` → tüm property’leri **salt-okunur** yapar.
- Kullanım alanı: **immutable objeler**, **config ayarları**, **fonksiyon parametre güvenliği**.