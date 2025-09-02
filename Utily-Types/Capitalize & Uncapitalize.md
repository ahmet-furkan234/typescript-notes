
## 🔹 `Capitalize<S>` Nedir?

`Capitalize<S>` → Bir string literal tipinin **ilk harfini büyük** yapar.

- `S` → string literal tip

📌 Tanımı (TypeScript içinde):

```ts
type Capitalize<S extends string> = intrinsic;
```

---

## 🔹 `Uncapitalize<S>` Nedir?

`Uncapitalize<S>` → Bir string literal tipinin **ilk harfini küçük** yapar.

- `S` → string literal tip

```ts
type Uncapitalize<S extends string> = intrinsic;
```

---

## 🔹 Örnekler

### 1. Capitalize

```ts
type A = "hello";
type B = Capitalize<A>;
// type B = "Hello"
```

### 2. Uncapitalize

```ts
type A = "World";
type B = Uncapitalize<A>;
// type B = "world"
```

---

### 3. Union tiplerde

```ts
type Words = "apple" | "banana" | "cherry";

type CapitalWords = Capitalize<Words>;
// "Apple" | "Banana" | "Cherry"

type UncapitalWords = Uncapitalize<"X" | "Y" | "Z">;
// "x" | "y" | "z"
```

---

### 4. Karma stringler

```ts
type Greeting = "helloWorld";

type CapitalGreeting = Capitalize<Greeting>;
// "HelloWorld"

type UncapitalGreeting = Uncapitalize<"HelloWorld">;
// "helloWorld"
```

---

### 5. API/Key mapping senaryosu

```ts
type Keys = "userId" | "userName";

type CapitalKeys = Capitalize<Keys>;
// "UserId" | "UserName"

type UncapitalKeys = Uncapitalize<"AdminId" | "AdminName">;
// "adminId" | "adminName"
```

- Özellikle **camelCase / PascalCase dönüşümlerinde** veya **string key normalization** için kullanışlıdır.

---

## 🔹 Kullanım Senaryoları

- **CamelCase veya PascalCase tiplerini oluşturmak**
- **Union tiplerde tek case standardı sağlamak**
- **API key veya frontend-backend mapping**

---

✅ Özet:

- `Capitalize<S>` → string literal tipinin **ilk harfini büyük yapar**
- `Uncapitalize<S>` → string literal tipinin **ilk harfini küçük yapar**
- Union tiplerde ve string key mapping senaryolarında çok işe yarar
