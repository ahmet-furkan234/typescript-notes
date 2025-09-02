
## 🔹 `Uppercase<S>` Nedir?

`Uppercase<S>` → Bir string literal tipini **büyük harfe çevirir**.

- `S` → string literal tip (ör: `"hello"`)

📌 Tanımı (TypeScript içinde):

```ts
type Uppercase<S extends string> = intrinsic;
```

- `intrinsic` → TypeScript’in yerleşik string literal dönüşüm mekanizması

---

## 🔹 `Lowercase<S>` Nedir?

`Lowercase<S>` → Bir string literal tipini **küçük harfe çevirir**.

- `S` → string literal tip

```ts
type Lowercase<S extends string> = intrinsic;
```

---

## 🔹 Örnekler

### 1. Uppercase

```ts
type A = "hello";
type B = Uppercase<A>;
// type B = "HELLO"
```

### 2. Lowercase

```ts
type A = "WORLD";
type B = Lowercase<A>;
// type B = "world"
```

---

### 3. Union tiplerde

```ts
type Letters = "a" | "b" | "c";

type UpperLetters = Uppercase<Letters>;
// "A" | "B" | "C"

type LowerLetters = Lowercase<"X" | "Y" | "Z">;
// "x" | "y" | "z"
```

---

### 4. Literal string kombinasyonları

```ts
type Greeting = "Hello World";

type UpperGreeting = Uppercase<Greeting>;
// "HELLO WORLD"

type LowerGreeting = Lowercase<Greeting>;
// "hello world"
```

---

### 5. API/Key mapping senaryosu

```ts
type APIKeys = "userId" | "userName";

type UpperAPIKeys = Uppercase<APIKeys>;
// "USERID" | "USERNAME"

type LowerAPIKeys = Lowercase<APIKeys>;
// "userid" | "username"
```

- Özellikle **string literal union tipleri ile enum veya sabit key mapping** için çok kullanışlıdır.
    

---

## 🔹 Kullanım Senaryoları

- **String literal tiplerini normalize etmek** (örn. enum veya key mapping)
- **API response’larıyla uyumlu tipler oluşturmak**
- **Union tiplerde tek bir case standardı sağlamak**

---

✅ Özet:

- `Uppercase<S>` → string literal tipini **büyük harfe çevirir**
- `Lowercase<S>` → string literal tipini **küçük harfe çevirir**
- Union tiplerde ve string key mapping senaryolarında çok kullanışlıdır
