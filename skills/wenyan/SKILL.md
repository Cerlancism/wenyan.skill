---
name: wenyan
description: "Write, read, debug, and compile wenyan-lang (文言) code — a programming language using Classical Chinese grammar that compiles to JavaScript, Python, or Ruby. Use this skill whenever the user asks about wenyan-lang, Classical Chinese programming, writing .wy files, debugging wenyan code, translating between wenyan and JS/Python/Ruby, or mentions 文言 programming. Also trigger when user mentions wenyan syntax like 吾有, 書之, 施...於, or asks to write code in ancient/classical Chinese. Also handles migrating existing TypeScript/JavaScript/Python/Ruby codebases to wenyan-lang — trigger when user asks to convert, migrate, port, or translate existing code to wenyan."
---

# 文言編程術

文言者，以古漢語文法編程，編譯至JS/Python/Ruby。代碼如古文。

## 職

助撰、讀、調試、編譯文言代碼。能：
- 依規格或偽代碼撰新文言程式
- 文言↔JS/Python/Ruby雙向譯
- 讀編譯輸出或錯誤訊息以調試
- 以自然語言釋文言代碼
- 遷移既有TS/JS/Python/Ruby代碼庫至文言

## 速查

撰文言前，先熟此要。詳見`references/`。

### 型

| 型 | 關鍵字 | 值 |
|------|---------|--------|
| 數值 | `數` | `三`, `一百二十`, `三點一四` |
| 字串 | `言` | `「「text」」`（雙角括號）|
| 布爾 | `爻` | `陽`(true), `陰`(false) |
| 數組 | `列` | **1起始！** |
| 對象 | `物` | 鍵值對 |
| 自動 | `元` | 編譯器推斷型 |

### 宣告

```
吾有一數。曰三。名之曰「x」。          // var x = 3
吾有一言。曰「「hello」」。名之曰「s」。  // var s = "hello"
吾有一爻。曰陰。名之曰「b」。           // var b = false
吾有一列。名之曰「arr」。               // var arr = []
吾有一物。名之曰「obj」。               // var obj = {}
有數五十。名之曰「n」。                 // var n = 50（簡寫）
```

多變量宣告：
```
吾有三數。曰一。曰三。曰五。名之曰「甲」曰「乙」曰「丙」。
```

重賦值：
```
昔之「x」者。今「y」是矣。              // x = y
```

### 流程控制

```
若「x」大於「y」者。                    // if (x > y) {
  ⋯⋯
也。                                   // }

若非。                                 // else {
  ⋯⋯
也。

為是十遍。⋯⋯云云。                     // for (i=0; i<10; i++) {...}
恆為是。⋯⋯云云。                       // while (true) {...}
凡「arr」中之「item」。⋯⋯云云。          // for (var item of arr) {...}
乃止。                                 // break
```

比較：`大於`、`不大於`、`小於`、`不小於`、`等於`、`不等於`

### 算術

```
加「x」以「y」。    // x + y
減「x」以「y」。    // x - y
乘「x」以「y」。    // x * y
除「x」以「y」。    // x / y
除「x」以「y」。所餘幾何。  // x % y
```

注意：`加X以Y`→X+Y，`加X於Y`→Y+X（於反序）

### 邏輯

```
夫「a」「b」中有陽乎。    // a || b
夫「a」「b」中無陰乎。    // a && b
變「x」。               // !x（取反）
```

### 術（函數）

定義：
```
吾有一術。名之曰「fn」。欲行是術。必先得一數。曰「x」。乃行是術曰。
  加「x」以一。名之曰「result」。
  乃得「result」。
是謂「fn」之術也。
```

調用：
```
施「fn」於「arg」。                // fn(arg)
施「fn」於「a」於「b」。           // fn(a, b)——自動柯里化！
```

返回：
```
乃得「x」      // return x
乃得矣        // return（末表達式）
乃歸空無       // return（空）
```

### 棧式嵌套調用

`夫`入棧，`取N以施「fn」`出N項調fn：
```
夫「a」。夫「b」。夫「c」。取二以施「f」。取二以施「g」。名之曰「result」。
// result = g(a, f(b, c))
```

棧特殊變量：
- `其`→最近無名結果（兼清棧）
- `噫`→棄/清無名棧

### 列（1起始！）

```
充「arr」以四。以二。              // arr.push(4, 2)
銜「a」以「b」。                  // a.concat(b)
夫「arr」之一。                   // arr[0]（1起始→JS 0起始）
夫「arr」之其餘。                 // arr.slice(1)
夫「obj」之「「key」」。           // obj["key"]
夫「arr」之長。                   // arr.length
```

### 物（對象）

```
吾有一物。名之曰「obj」。其物如是。物之「「name」」者。言曰「「Alice」」。物之「「age」」者。數曰三十。是謂「obj」之物也。
// obj = {name: "Alice", age: 30}
```

### 導入導出

```
吾嘗觀「「算經」」之書。方悟「正弦」「餘弦」之義。
// import {sin, cos} from "math"
```

- `今有`→導出（公）
- `吾有`→私有（域內）

### 錯誤處理

```
姑妄行此。                        // try {
  ⋯⋯
如事不諧。豈「「異類」」之禍歟。名之曰「e」。   // } catch(e) if TypeError
  ⋯⋯
不知何禍歟。名之曰「e」。           // catch any
  ⋯⋯
乃作罷。                          // }
```

拋出：`嗚呼。「「ErrorName」」之禍。曰「「message」」`
內建型：`文法`(Syntax)、`逾界`(Range)、`異類`(Type)、`虛指`(Reference)

### 注釋

```
批曰。「「注釋文」」。
注曰。「「注釋文」」。
疏曰。「「注釋文」」。
```

### 巨集

```
或云「「書「甲」焉」」。
蓋謂「「吾有一言。曰「甲」。書之」」。
```

### 輸出

```
書之。    // console.log（印棧上無名值）
```

### 自動柯里化

文言函數皆自動柯里化。部分應用返新函數：
```
施「f」於「a」於「b」。名之曰「partial」。   // partial = f(a)(b)
施「partial」於「c」。                      // partial(c) = f(a)(b)(c)
```

## 代碼庫遷移（TS/JS/Python/Ruby → 文言）

遷移既有代碼至文言。逐檔或批量皆可。

### 流程

1. **分析源碼**——讀源檔，識別函數、類、模塊結構、依賴關係
2. **規劃遷移序**——依賴圖底→上：先無依賴模塊，後依賴者
3. **逐模塊轉譯**——每模塊：
   - 源函數→文言術（`吾有一術`）
   - 源類→文言物+術組合
   - 源型→文言型對應（見型對照表）
   - 保持導入導出結構（`吾嘗觀…之書`/`今有`）
4. **編譯驗證**——每轉一模塊即`npx wenyan -c`驗證
5. **執行測試**——`npx wenyan file.wy`跑結果，與源碼輸出比對

### 型對照

| TS/JS | Python | Ruby | 文言 |
|-------|--------|------|------|
| `number` | `int`/`float` | `Integer`/`Float` | `數` |
| `string` | `str` | `String` | `言` |
| `boolean` | `bool` | `TrueClass`/`FalseClass` | `爻` |
| `Array<T>` / `list` | `list` | `Array` | `列`（**1起始！**）|
| `object` / `Record` | `dict` | `Hash` | `物` |
| `any` | `Any` | — | `元` |

### 模式對照

| 源碼模式 | 文言等價 |
|----------|----------|
| `function f(x) { return x+1 }` | `吾有一術。名之曰「f」。欲行是術。必先得一數。曰「x」。乃行是術曰。加「x」以一。乃得其。是謂「f」之術也。` |
| `class Foo { constructor(x) {...} method() {...} }` | 物+多術組合（文言無類，以物模擬）|
| `import {a} from 'b'` | `吾嘗觀「「b」」之書。方悟「a」之義。` |
| `export function f()` | `今有一術。名之曰「f」。`（`今有`=公開）|
| `try/catch` | `姑妄行此。⋯如事不諧。⋯乃作罷。` |
| `for (let x of arr)` | `凡「arr」中之「x」。⋯云云。` |
| `arr.push(v)` | `充「arr」以「v」。` |
| `arr[i]` | `夫「arr」之N。`（N=i+1，1起始！）|
| `console.log(x)` | `吾有一言。曰「x」。書之。` 或棧上值直接`書之。` |

### 限制與注意

- **無類語法**——類需拆為物+術，方法作獨立術
- **無async/await**——異步代碼需重構為同步或回調
- **無泛型**——用`元`型或重複定義
- **列1起始**——所有索引+1，`arr[0]`→`夫「arr」之一`
- **無三元運算**——展開為`若…也。若非…也。`
- **標準庫差異**——查`references/stdlib.md`尋等價函數，無等價者需自撰
- **無原型鏈/繼承**——扁平化對象結構

### 遷移策略建議

- **小型腳本**（<200行）→一次全轉
- **中型模塊**（200-1000行）→逐函數轉，每函數驗證
- **大型代碼庫**（>1000行）→先遷核心邏輯模塊，外圍保留JS互操作
- **含外部依賴**→依賴留JS，文言通過`吾嘗觀…之書`引入編譯後JS

## 編譯與測試

```bash
npx wenyan file.wy              # 編譯並執行
npx wenyan -c file.wy           # 僅編譯→JS stdout
npx wenyan -c -l py file.wy     # 編譯→Python
npx wenyan -c -l rb file.wy     # 編譯→Ruby
npx wenyan -e '吾有一言。曰「「問天地好在」」。書之。'  # 行內求值
npx wenyan -c --roman pinyin file.wy  # 羅馬化標識符
```

撰文言後必驗：
1. 寫.wy檔
2. `npx wenyan -c file.wy`驗編譯
3. `npx wenyan file.wy`測執行
4. 有錯→讀編譯JS以調試

## 常見陷阱

1. **列1起始**——`夫「arr」之一`=JS之arr[0]
2. **字串需雙角括號**——`「「text」」`非`「text」`
3. **變量名用單角括號**——`「varname」`
4. **`也`結條件塊；`云云`結循環**
5. **`矣`用於塊外重賦值；`也`用於若/若非塊內**
6. **`其`清棧**——連用多`其`易混，不宜
7. **標點可省**——然加之益讀
8. **`今有`為公/導出**——私用`吾有`

## 參考文件

速查之外詳參：
- `references/syntax.md`——語法全表，wenyan↔JS對照
- `references/stdlib.md`——標準庫函數（算經、列經、易經等）
- `references/patterns.md`——常見模式、慣用法、進階範例

需詳情時讀之（如特定stdlib函數、進階巨集、複雜嵌套調用）。
