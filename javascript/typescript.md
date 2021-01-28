# Dynamic Typed Languages vs. Static Typed Languages
| | Dynamic | Static
--- | --- | ---
Definition | don't have to declare the type of variable | has to declare explictily the type of variable before using it
Typechecking | runtime | compile time
Advantages | - less time debugging syntax and semantic errors;<br>- more flexibility;<br>- write software faster; | - self-documentation;<br>- helps with auto completion;<br>- less bugs in production
Disadvantages | - more prone to runtime errors and bugs; | - code harder to read;<br>- harder to learn;<br>- easy to forget we still need good tests;<br>- slower development process;

Weakly and strongly typed terms are often confused with dynamic and static. With the following example:
```
var a = 'something'
a + 17
```
In a weakly typed language we would get back a string `'something17'`, while on a strong typed language we would get an error.\
JavaScript is a dynamic language that is weakly typed.

# TypeScript
__TypeScript__ → allows JavaScript to behave like a static-typed language, making it extra safe.

There are other languages that turn JavaScript into a static-tyed language. The main difference between them is the compiler.
- __flow__ → static type checker. Depends on Babel to transform the code to valid JS code, and only on files we say to check.
- __TypeScript__ → JavaScript superset - it adds functionality on top of JavaScript. It has its own compiler.
- __ReasonML__ & __ELM__ → completely a separate language from JavaScript. It also has its own compiler.

The growth of TypeScript has been far superior from all the others.

_Installing TypeScript compiler globally:_
```
$ sudo npm install -g typescript
```

_Running the compiler:_
```
$ tsc [options] index.ts
```
- `--watch` → run in watch mode. It will watch for changes and recompile the files everytime it detects a change.
TypeScript files have a *.ts* extension.

_Initialize project as a TypeScript project:_
```
$ tsc --init
```
A configuration file will be generated. It allows us to control the compiler's behavior.

## TypeScript Types
`boolean`, `number`, `string`, `string[]` or `Array<string>`, `object`, `undefined`, `null`, tuple, `Enum`, `any`, `void`, `unknown`, `never`, `interface`, `type`, union

There are several times where a explicit mention of a type is not necessary. TypeScript can infer it.
```typescript
let num = 2
num = 'hello' // error
```

### `interface` vs `type`
Although interfaces and types can kinda act in the same way, there are three key differences:
- we cannot use `implements` on a class if we use the `union` operator within our type definition;
- we cannot use `extends` on a class if we use the `union` operator within our type definition;
- declaration merging doesn't work with type alias.

We can use whichever best suits us. However we should always use `interface` for public API's definitions when authoring a library, and we should consider using `type` for our React Compenent Props and State since it avoids monkey patching.

## Type Assertions
Allows us to override an inferred and analyzed view of types in any way we want. We are basically saying the compiler we know the types better than it does, and it should not second guess us.

```typescript
interface Foo {
  id: number,
  name: string
}
const foo = {} as Foo
foo.id = 123
foo.name = 'something'
```

A type assertion **is not considered type casting**, since *casting* generally implies some sort of runtime support. Type assertions are purely a compile type construct.

We should be carefully when using type assertions, since the compiler will not protect us from forgetting to add properties we promised.

A good use case for type assertions is when the user thinks the event passed in will be a more specific case of an event:
```typescript
function handler(event: Event) {
  const mouseEvent = event as MouseEvent;
}
```

### Double Assertions
If we pass a completely wild assertion, *e.g.* try to type assert an `Event` to a `HTMLElement`, TypeScript will complain. To stop the compiler from complaining, we need to make a double assertion, with one of the types as `unknown` or `any`:
```typescript
function handle(event: Event) {
  const element = event as unknown as HTMLElement
}
```
The assertion from type `S` to `T` succeeds if either `S` is a subtype of `T`, or `T` a subtype of `S`. This is the reason why we need to use `unknown` in this case. However **this is unsafe**, and should be avoided if possible.

### Classes
With TypeScript, it's possible to set a class property to `private`. It will make the property unreadable outside of the class.
```typescript
class Animal {
  private sing: string = 'lalala'
  constructor(sound: string) {
    this.sing = sound
  }
  // ...
}

const lion = new Animal('RAAWWR')
lion.sing // Error is thrown
```

## Type Definitions
TypeScript allows us to use **declaration files** - files that allow us to describe the shape of code that is written in it. It comes in handy when using libraries that do not natively support TypeScript, *e.g* React, jQuery.

[Definitely Typed](https://definitelytyped.org/) is a repository for TypeScript type definitions. It contains declaration files for third party libraries.

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie\
[Interface vs Type alias in TypeScript 2.7 – Medium](https://medium.com/@martin_hotell/interface-vs-type-alias-in-typescript-2-7-2a8f1777af4c)\
[Type Assertion – TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/type-assertion)
