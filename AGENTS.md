# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 項目

AI agent skill→教agent讀寫調試遷移wenyan-lang（文言）代碼。文言以古漢語文法編程，編譯至JS/Python/Ruby。含既有TS/JS/Python/Ruby代碼庫→文言遷移能力。

## 命令

```bash
npm install                              # 安裝依賴（@wenyan/cli）
npx wenyan file.wy                       # 編譯並執行.wy
npx wenyan -c file.wy                    # 僅編譯→stdout JS
npx wenyan -c -l py file.wy              # 編譯→Python
npx wenyan -c -l rb file.wy              # 編譯→Ruby
npx wenyan -e '吾有一言。曰「「問天地好在」」。書之。'  # 行內求值
npx wenyan -r file.wy                    # 渲染輸出
npx wenyan -c --roman pinyin file.wy     # 羅馬化標識符
npx wenyan -i                            # 交互REPL
```

## 架構

```
skills/wenyan/                  # 已建skill（agent消費端）
  SKILL.md                      # skill主定義——語法速查、遷移指南、編譯指令
  references/
    syntax.md                   # 語法全表 wenyan↔JS對照
    stdlib.md                   # 標準庫函數
    patterns.md                 # 常見模式與慣用法
.agents/skills/humanizer/       # 第三方skill（blader/humanizer）
references/                     # gitignored，僅.keep受版控
  .keep                         # 佔位檔，確保目錄存在
  wenyan.wiki/                  # wenyan-lang wiki全文（語言規範語料）——需手動clone
  wenyan/                       # wenyan-lang repo文檔+示例——需手動clone
package.json                    # devDep: @wenyan/cli用於編譯驗證
skills-lock.json                # 第三方skill版本鎖
```

核心交付物為`skills/wenyan/SKILL.md`——agent靠此檔學文言語法、編譯流程、代碼遷移。`references/`為原始語料（gitignored），SKILL.md為精煉後agent可消費之速查。

## 設置

```bash
npm install                                                          # 安裝依賴
git clone https://github.com/wenyan-lang/wenyan.wiki.git references/wenyan.wiki  # clone wiki
git clone https://github.com/wenyan-lang/wenyan.git references/wenyan            # clone repo
```

`references/`下除`.keep`外皆被gitignore，clone後不會影響版控。

## 參考文檔

文言語言文檔在`references/wenyan.wiki/`。要文：

- **Syntax-Cheatsheet.md** — 語法全表，wenyan↔JS對照
- **Variables.md** — 型（數/言/爻/列/物/元）、宣告、賦值
- **Function-Call.md** — 棧式嵌套調用、自動柯里化
- **Error-Handling.md** — try/catch（姑妄行此/如事不諧/乃作罷）
- **Importing.md** — 模塊（吾嘗觀…之書/今有=導出/吾有=私有）
- **Macros.md** — 語法糖（或云/蓋謂）
- **Standard-Library-Cheatsheet.md** — 標準庫
- **Compiler-API.md** — `@wenyan/core` compile()/execute() API

## 文言速查

### 核心語法

| 文言 | 義 |
|---|---|
| `吾有一數。曰三。名之曰「甲」。` | `var a = 3` |
| `吾有一言。曰「「text」」。名之曰「乙」。` | `var b = "text"` |
| `吾有一爻。曰陰。` | `var x = false`（陽=true）|
| `吾有一列。名之曰「甲」。` | `var a = []` |
| `吾有一物。名之曰「甲」。` | `var a = {}` |
| `昔之「甲」者。今「乙」是矣。` | `a = b`（重賦值）|
| `若X大於Y者。⋯⋯也。` | `if (X > Y) { ... }` |
| `若非。⋯⋯也。` | `else { ... }` |
| `為是N遍。⋯⋯云云。` | `for (i=0; i<N; i++) { ... }` |
| `恆為是。⋯⋯云云。` | `while (true) { ... }` |
| `凡「甲」中之「乙」。⋯⋯云云。` | `for (var b of a) { ... }` |
| `乃止。` | `break` |
| `加X以Y。`/`減X以Y。` | `X+Y`/`X-Y` |
| `乘X以Y。`/`除X以Y。` | `X*Y`/`X/Y` |
| `書之。` | `console.log(...)` |
| `乃得X` | `return X` |
| `乃歸空無` | `return` |

### 術（函數）

```
吾有一術。名之曰「fn」。欲行是術。必先得一數。曰「甲」。乃行是術曰。
  ⋯⋯
是謂「fn」之術也。

施「fn」於「甲」。    // fn(a)
```

### 導入導出

```
吾嘗觀「「算經」」之書。方悟「正弦」「餘弦」之義。  // import {sin,cos} from "math"
今有一術。名之曰「公開fn」。  // 今有=exported，吾有=private
```

### 要則

- 列（數組）**1起始**
- 標點換行皆可省（如古文）
- 字串用`「「…」」`（雙角括號）
- 變量名用`「…」`（單角括號）
- `其`→最近無名結果（兼清棧）
- `噫`→清無名變量棧
- 函數自動柯里化
- 型：數(number) 言(string) 爻(boolean) 列(array) 物(object) 元(auto)

## 編輯規範

- 改README時須同步更新所有語言版本（README.md、README.en.md）
