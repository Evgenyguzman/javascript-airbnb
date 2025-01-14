# TypeScript Style Guide and Coding Conventions

Key Sections:

- [Variable](#variable-and-function)
- [Class](#class)
- [Interface](#interface)
- [Type](#type)
- [Namespace](#namespace)
- [Enum](#enum)
- [`null` vs. `undefined`](#null-vs-undefined)
- [Formatting](#formatting)
- [Single vs. Double Quotes](#quotes)
- [Tabs vs. Spaces](#spaces)
- [Use semicolons](#semicolons)
- [Annotate Arrays as `Type[]`](#array)
- [File Names](#filename)
- [`type` vs `interface`](#type-vs-interface)

## Variable and Function

- Use `camelCase` for variable and function names

> Reason: Conventional JavaScript

**Плохо**

```ts
var FooVar;
function BarFunc() {}
```

**Хорошо**

```ts
var fooVar;
function barFunc() {}
```

## Class

- Use `PascalCase` for class names.

> Reason: This is actually fairly conventional in standard JavaScript.

**Плохо**

```ts
class foo {}
```

**Хорошо**

```ts
class Foo {}
```

- Use `camelCase` of class members and methods

> Reason: Naturally follows from variable and function naming convention.

**Плохо**

```ts
class Foo {
  Bar: number;
  Baz() {}
}
```

**Хорошо**

```ts
class Foo {
  bar: number;
  baz() {}
}
```

## Interface

- Use `PascalCase` for name.

> Reason: Similar to class

- Use `camelCase` for members.

> Reason: Similar to class

- **Не** используй префикс `I` для интерфейсоов

> Reason: Unconventional. `lib.d.ts` defines important interfaces without an `I` (e.g. Window, Document etc).

**Плохо**

```ts
interface IFoo {}
```

**Хорошо**

```ts
interface Foo {}
```

## Type

- Use `PascalCase` for name.

> Reason: Similar to class

- Use `camelCase` for members.

> Reason: Similar to class

## Namespace

- Use `PascalCase` for names

> Reason: Convention followed by the TypeScript team. Namespaces are effectively just a class with static members. Class names are `PascalCase` => Namespace names are `PascalCase`

**Плохо**

```ts
namespace foo {}
```

**Хорошо**

```ts
namespace Foo {}
```

## Enum

- Use `PascalCase` for enum names

> Reason: Similar to Class. Is a Type.

**Плохо**

```ts
enum color {}
```

**Хорошо**

```ts
enum Color {}
```

- Use `PascalCase` for enum member

> Reason: Convention followed by TypeScript team i.e. the language creators e.g `SyntaxKind.StringLiteral`. Also helps with translation (code generation) of other languages into TypeScript.

**Плохо**

```ts
enum Color {
  red,
}
```

**Хорошо**

```ts
enum Color {
  Red,
}
```

## Null vs. Undefined

- Prefer not to use either for explicit unavailability

> Reason: these values are commonly used to keep a consistent structure between values. In TypeScript you use _types_ to denote the structure

**Плохо**

```ts
let foo = { x: 123, y: undefined };
```

**Хорошо**

```ts
let foo: { x: number; y?: number } = { x: 123 };
```

- Use `undefined` in general (do consider returning an object like `{valid:boolean, value?:Foo}` instead)

**Плохо**

```ts
return null;
```

**Хорошо**

```ts
return undefined;
```

- Use `null` where it's a part of the API or conventional

> Reason: It is conventional in Node.js e.g. `error` is `null` for NodeBack style callbacks.

**Плохо**

```ts
cb(undefined);
```

**Хорошо**

```ts
cb(null);
```

- Use _truthy_ check for **objects** being `null` or `undefined`

**Плохо**

```ts
if (error === null)
```

**Хорошо**

```ts
if (error)
```

- Use `== null` / `!= null` (not `===` / `!==`) to check for `null` / `undefined` on primitives as it works for both `null`/`undefined` but not other falsy values (like `''`, `0`, `false`) e.g.

**Плохо**

```ts
if (error !== null) // does not rule out undefined
```

**Хорошо**

```ts
if (error != null) // rules out both null and undefined
```

## Quotes

- Prefer single quotes (`'`) unless escaping.

> Reason: More JavaScript teams do this (e.g. [airbnb](https://github.com/airbnb/javascript), [standard](https://github.com/feross/standard), [npm](https://github.com/npm/npm), [node](https://github.com/nodejs/node), [google/angular](https://github.com/angular/angular/), [facebook/react](https://github.com/facebook/react)). It's easier to type (no shift needed on most keyboards). [Prettier team recommends single quotes as well](https://github.com/prettier/prettier/issues/1105)

> Double quotes are not without merit: Allows easier copy paste of objects into JSON. Allows people to use other languages to work without changing their quote character. Allows you to use apostrophes e.g. `He's not going.`. But I'd rather not deviate from where the JS Community is fairly decided.

- When you can't use double quotes, try using back ticks (\`).

> Reason: These generally represent the intent of complex enough strings.

## Spaces

- Use `2` spaces. Not tabs.

> Reason: More JavaScript teams do this (e.g. [airbnb](https://github.com/airbnb/javascript), [idiomatic](https://github.com/rwaldron/idiomatic.js), [standard](https://github.com/feross/standard), [npm](https://github.com/npm/npm), [node](https://github.com/nodejs/node), [google/angular](https://github.com/angular/angular/), [facebook/react](https://github.com/facebook/react)). The TypeScript/VSCode teams use 4 spaces but are definitely the exception in the ecosystem.

## Semicolons

- Use semicolons.

> Reasons: Explicit semicolons helps language formatting tools give consistent results. Missing ASI (automatic semicolon insertion) can trip new devs e.g. `foo() \n (function(){})` will be a single statement (not two). TC39 [warning on this as well](https://github.com/tc39/ecma262/pull/1062). Example teams: [airbnb](https://github.com/airbnb/javascript), [idiomatic](https://github.com/rwaldron/idiomatic.js), [google/angular](https://github.com/angular/angular/), [facebook/react](https://github.com/facebook/react), [Microsoft/TypeScript](https://github.com/Microsoft/TypeScript/).

## Array

- Annotate arrays as `foos: Foo[]` instead of `foos: Array<Foo>`.

> Reasons: It's easier to read. It's used by the TypeScript teams. Makes easier to know something is an array as the mind is trained to detect `[]`.

## Filename

Name files with `camelCase`. E.g. `accordion.tsx`, `myControl.tsx`, `utils.ts`, `map.ts` etc.

> Reason: Conventional across many JS teams.

## type vs. interface

- Use `type` when you _might_ need a union or intersection:

```
type Foo = number | { someProperty: number }
```

- Use `interface` when you want `extends` or `implements` e.g.

```
interface Foo {
  foo: string;
}
interface FooBar extends Foo {
  bar: string;
}
class X implements FooBar {
  foo: string;
  bar: string;
}
```

- Otherwise use whatever makes you happy that day.
