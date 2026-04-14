# 文言 (Wenyan) Skill

> [中文文檔](README.md)

An AI agent's craft: to pen, read, mend, and transmute wenyan-lang (文言) code.

Wenyan hath Classical Chinese for its tongue and a modern compiler for its hand. Each line may sound as a sentence; each function, as a little song. Yet when the play is done, it exits as JS, Python, or Ruby. This skill schools an agent to write from a brief, heed the compiler's rebuke, mend the broken line, and bear JS, Python, Ruby, or TypeScript code into wenyan by degrees. Source at [wenyan-lang](https://github.com/wenyan-lang/wenyan).

## Wherefore program in wenyan?

Wenyan asks for a slower eye. It folds branches, recursion, arrays, and objects back into clauses fit to be spoken. To read it is to parse a passage; to write it is to choose the word that must stand and no other.

- Chinese characters are compact vessels. For the same logic, wenyan source often spends fewer tokens than JS/Python, so agents have less to summon and less to read
- Names such as 甲, 乙, 加, 減, and 求 sit close to the meaning, as if born in the sentence itself
- Unfamiliar syntax bids thee look again at control flow, types, and indexing, lest habit play the scribe in thy stead
- Classical phrasing gives the program music: conditions, returns, and loops read as close-set clauses rather than boilerplate
- Wenyan compiles to JS/Python/Ruby, so thou mayst try one small module before remaking the whole codebase

```wenyan
吾有一術。名之曰「階乘」。欲行是術。必先得一數。曰「甲」。乃行是術曰。
	若「甲」不大於一者。乃得一。也。
	減「甲」以一。施「階乘」於其。乘「甲」以其。乃得其。
是謂「階乘」之術也。

施「階乘」於五。書之。
```

Here stands factorial in a few lines: the function calls itself, the `若` clause returns one, and subtraction and multiplication keep their places between.

## Install

```bash
npx skills add Cerlancism/wenyan.skill/skills/wenyan
```

Choose thine agent:

```bash
npx skills add Cerlancism/wenyan.skill/skills/wenyan -a claude-code
npx skills add Cerlancism/wenyan.skill/skills/wenyan -a codex
```

Install it for every project:

```bash
npx skills add Cerlancism/wenyan.skill/skills/wenyan -g
```

After install, the skill definition is at `.agents/skills/wenyan/SKILL.md` and references are at `.agents/skills/wenyan/references/`.

For more install options, run `npx skills add --help`.

## What it does

- Writes wenyan programs from specs or pseudocode
- Translates both ways between wenyan and JS/Python/Ruby
- Reads compiler output and error messages, then helps locate and fix issues
- Converts TypeScript/JavaScript/Python/Ruby code to wenyan in small steps, including type mapping, index offset changes, and class decomposition

## Usage

Requires Node.js.

```bash
npm install
npx wenyan -e '吾有一言。曰「「問天地好在」」。書之。'
# => 問天地好在
```

## Examples

Hello World:

```wenyan
吾有一數。曰三。名之曰「甲」。
為是「甲」遍。
	吾有一言。曰「「問天地好在。」」。書之。
云云。
```

Prints "問天地好在。" three times, as though one called to heaven and earth and heard the line return.

Fibonacci:

```wenyan
吾有二數。曰零。曰一。名之曰「甲」曰「乙」。
為是百遍。
	加「甲」以「乙」。名之曰「丙」。
	昔之「甲」者。今「乙」是矣。
	昔之「乙」者。今「丙」是矣。
云云。
書「乙」。
```

## Migration example

TypeScript -> wenyan:

```typescript
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

For larger codebases, migrate module by module, as one might sort bamboo slips bundle by bundle. Common adjustments include type mapping (`number` -> 數, `string` -> 言, etc.), 0-based to 1-based index offsets, and class -> object+function decomposition.

## References

- [Language Spec](https://wy-lang.org/spec)
- [Online IDE](https://ide.wy-lang.org/)
- [Intro Book 《文言陰符》](https://github.com/wenyan-lang/book)
- [Syntax Cheatsheet](https://github.com/wenyan-lang/wenyan/wiki/Syntax-Cheatsheet)

## License

MIT
