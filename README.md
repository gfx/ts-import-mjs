# TypeScript compiler requires *.mts to import *.mjs

TypeScript compiler (tsc) requires `*.mts` to import `*.mjs` files, but Deno requires `*.mjs` to import `*.mts` files. How can I make a TypeScript file that both tsc and Deno compile?

## Details

File `./foo.mts`:


```typescript
export function hello() {
    console.log("hello");
}
```

File `./index.mts`:

```typescript
import { hello } from './foo.mjs';

hello();
```

ts-node:

```
$ npx ts-node --esm src/index.mts
hello
```

deno run:
```
$ deno --version
deno 1.29.1 (release, aarch64-apple-darwin)
v8 10.9.194.5
typescript 4.9.4
$ deno run src/index.mts
error: Module not found "file:///path/to/ts-import-mjs/src/foo.mjs".
    at file:///path/to/ts-import-mjs/src/index.mts:1:23
```
