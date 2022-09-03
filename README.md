# template.ts

TypeScript template repository.

---

Run initial setup:

```sh
npm init
```

Install dependencies:

```sh
npm install --save-dev \
  @rollup/plugin-eslint @rollup/plugin-typescript \
  @typescript-eslint/eslint-plugin @typescript-eslint/parser \
  esbuild eslint npm-run-all rimraf rollup \
  rollup-plugin-bundle-size rollup-plugin-dts rollup-plugin-esbuild \
  typescript
```

Install testing dependencies:

```sh
npm install --save-dev @types/chai @types/mocha chai esbuild-runner mocha
```

If Node module type declarations are required, include:

```sh
npm install --save-dev @types/node
```

---

Example for `package.json`:

```json
{
  "sideEffects": false,
  "type": "module",
  "exports": {
    "import": "./lib/index.mjs",
    "require": "./lib/index.cjs",
    "default": "./lib/index.mjs"
  },
  "main": "lib/index.cjs",
  "jsdelivr": "lib/index.umd.min.js",
  "unpkg": "lib/index.umd.min.js",
  "module": "lib/index.mjs",
  "types": "lib/index.d.ts",
  "files": ["lib"],
  "scripts": {
    "prebuild": "rimraf lib",
    "build": "node scripts/build",
    "build:js": "esbuild src/index.ts",
    "build:rollup": "rollup -c",
    "check": "npm-run-all -p lint:strict ts",
    "lint": "eslint . --ext .js,.ts",
    "lint:fix": "npm run lint -- --fix",
    "lint:strict": "npm run lint -- --max-warnings 0",
    "start": "npm run build -- -w",
    "start:prod": "npm run build -- -w -p",
    "test": "npm-run-all -s test:mocha check",
    "test:mocha": "mocha -r esbuild-runner/register **/*.spec.ts",
    "test:watch": "npm run test:mocha -- --watch --watch-files src",
    "ts": "tsc --noEmit"
  }
}
```
