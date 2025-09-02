
## `Parameters<T>` Nedir?

➡️ **`Parameters<T>`**, bir fonksiyon tipinin parametre tiplerini **tuple (dizi)** olarak çıkartır.

- Yani fonksiyonun aldığı parametrelerin tiplerini alıp bir tuple’a dönüştürür.
- Eğer fonksiyonun hiç parametresi yoksa `[]` (boş tuple) döner.

📌 **Tanımı (TypeScript içinde)**:

```ts
type Parameters<T extends (...args: any) => any> = 
    T extends (...args: infer P) => any ? P : never;
```

Burada:

- `infer P` → parametrelerin tipini yakalar.
- Eğer `T` bir fonksiyon tipiyse `P` parametre tuple’ını döndürür.
- Fonksiyon değilse `never` döner.

---

## Örnekler

### 1. Basit kullanım

```ts
type Fn = (name: string, age: number) => boolean;

type Params = Parameters<Fn>;
// type Params = [name: string, age: number]
```

👉 `Params` artık `[string, number]` tipinde.

---

### 2. Hiç parametre almayan fonksiyon

```ts
type Fn = () => void;

type Params = Parameters<Fn>;
// type Params = []
```

---

### 3. Default ve opsiyonel parametreler

```ts
type Fn = (x: number, y?: string) => void;

type Params = Parameters<Fn>;
// type Params = [x: number, y?: string | undefined]
```

---

### 4. Gerçek fonksiyonlardan parametre tipini çıkarma

```ts
function createUser(id: number, name: string, isActive: boolean) {
  return { id, name, isActive };
}

type CreateUserParams = Parameters<typeof createUser>;
// type CreateUserParams = [id: number, name: string, isActive: boolean]

// Örnek kullanım:
const args: CreateUserParams = [1, "TkMatE", true];
const user = createUser(...args);
```

---

### 5. `never` dönen durum

```ts
type NotFunc = string;

type Params = Parameters<NotFunc>;
// type Params = never
```

Çünkü `string` bir fonksiyon tipi değildir.

---

## Kullanım Senaryoları

- **Fonksiyon parametrelerini yeniden kullanmak**:

    ```ts
    function login(username: string, password: string) {}
    type LoginParams = Parameters<typeof login>;
    // [username: string, password: string]
    
    function safeLogin(...args: LoginParams) {
      // aynı parametre tipleriyle
      return login(...args);
    }
    ```

- **Middleware veya wrapper yazarken** parametre tiplerini otomatik çıkartmak.
- **API function siganture’larını yeniden kullanmak**.

---

👉 Özet:  
`Parameters<T>`, bir fonksiyon tipinden parametreleri tuple olarak alıp başka yerde tekrar kullanmamıza yarar. Bu sayede parametre tanımlarını tekrar yazmadan **tip güvenliği** sağlar.
