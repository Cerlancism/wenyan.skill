# 文言 Skill

> [English](README.en.md)

教 AI agent 讀、寫、調試、遷移 wenyan-lang（文言）程式。

文言以古漢語為形，以現代編譯器為用：一行如短句，一術如小令，終可落成 JS、Python、Ruby。此 skill 讓 agent 能照規格成文、據錯誤修文，也能把既有 JS、Python、Ruby 或 TypeScript 代碼逐段移入文言。源碼見 [wenyan-lang](https://github.com/wenyan-lang/wenyan)。

## 為何用文言編程？

用文言寫程式，不只是給代碼披古衣。它把判斷、遞歸、列與物都壓回一句一句可誦的語勢裏；讀時像斷章句，寫時像鍛字。

- 漢字凝練。同等邏輯下，文言源碼常比 JS/Python 少耗 token，agent 生成與閱讀時也省些篇幅
- 變量名、術名貼近文義，如「甲」「乙」「加」「減」「求」，讀來像正文中自然生出的字
- 陌生句法會逼人重審控制流、資料型別與索引，不讓肌肉記憶代替思考
- 古語入算機，詩書之骨接上現代 runtime，本身便有一點奇氣
- 可編譯到 JS/Python/Ruby，適合先取一個小模塊試水，不必一開始就改整座代碼庫

```wenyan
吾有一術。名之曰「階乘」。欲行是術。必先得一數。曰「甲」。乃行是術曰。
	若「甲」不大於一者。乃得一。也。
	減「甲」以一。施「階乘」於其。乘「甲」以其。乃得其。
是謂「階乘」之術也。

施「階乘」於五。書之。
```

此即階乘：自調其術，若則歸一，減乘皆在數行間，字少而意足。

## 安裝 Skill

```bash
npx skills add Cerlancism/wenyan.skill
```

指定 agent：

```bash
npx skills add Cerlancism/wenyan.skill -a claude-code
npx skills add Cerlancism/wenyan.skill -a codex
```

全局安裝（所有項目可用）：

```bash
npx skills add Cerlancism/wenyan.skill -g
```

安裝後，skill 定義在 `.agents/skills/wenyan/SKILL.md`，參考資料在 `.agents/skills/wenyan/references/`。

更多安裝選項可查 `npx skills add --help`。

## 功能

- 依規格或偽代碼撰寫文言程式
- 在文言與 JS/Python/Ruby 之間雙向轉譯
- 讀編譯輸出與錯誤訊息，協助定位和修復問題
- 將 TypeScript/JavaScript/Python/Ruby 代碼逐步轉寫為文言，處理型映射、索引偏移和類拆解

## 用法

需要 Node.js。

```bash
npm install
npx wenyan -e '吾有一言。曰「「問天地好在」」。書之。'
# => 問天地好在
```

## 文言示例

Hello World：

```wenyan
吾有一數。曰三。名之曰「甲」。
為是「甲」遍。
	吾有一言。曰「「問天地好在。」」。書之。
云云。
```

印三次「問天地好在。」如叩天地而得回聲。

費波那契：

```wenyan
吾有二數。曰零。曰一。名之曰「甲」曰「乙」。
為是百遍。
	加「甲」以「乙」。名之曰「丙」。
	昔之「甲」者。今「乙」是矣。
	昔之「乙」者。今「丙」是矣。
云云。
書「乙」。
```

## 遷移示例

TypeScript -> 文言：

```typescript
// 源碼
function add(a: number, b: number): number {
  return a + b;
}
console.log(add(3, 5));
```

```wenyan
吾有一術。名之曰「加」。欲行是術。必先得二數。曰「甲」。曰「乙」。乃行是術曰。
	加「甲」以「乙」。乃得其。
是謂「加」之術也。

施「加」於三於五。書之。
```

大型代碼庫宜如理簡牘，逐卷而治。常見調整包括型映射（number -> 數、string -> 言等）、0 起始到 1 起始索引偏移，以及類 -> 物+術拆解。

## 參考

- [語言規範](https://wy-lang.org/spec)
- [線上IDE](https://ide.wy-lang.org/)
- [入門書《文言陰符》](https://github.com/wenyan-lang/book)
- [語法速查](https://github.com/wenyan-lang/wenyan/wiki/Syntax-Cheatsheet)

## 許可

MIT
