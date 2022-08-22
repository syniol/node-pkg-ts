# Creating Node.js Shared Packages using TypeScript
In this article you will learn everything needed to get started with 
writing your own private or open source package for Node.js in TypeScript.


## Initial Skeleton
Let's start by creating a new directory and enter the directory. Please run 
following command inside the root of your working directory.

> Please ensure new directory is empty before running the commands

    npm init -y
    npm install --save-dev typescript
    npx tsc --init

You should now see three additional files at the root of your working directory:
 * package.json
 * package-lock.json
 * tsconfig.json
and a folder `node_modules` containing our development dependency.

> npx command allows you to run executable CLI in your dependencies; in this case
we utilise it to run `tsc` with `--init` flag to create an initial `tsconfig.json`


## TypeScript Configuration
Initial `tsconfig.json` has many optional fields which are mostly out of scope of this
article. However, here we only mention bare minimum required options.

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "rootDir": "./src",
    "moduleResolution": "node",
    "declaration": true,
    "declarationMap": true,
    "outDir": "./dist",
    "inlineSourceMap": true,
    "declarationDir": "./dist/types",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true
  },
  "include": [
    "src/**/*.ts"
  ]
}
```

## Package Configuration

```json
{
  "main": "dist/index.js",
  "types": "./dist/types/index.d.ts",
  "scripts": {
    "build": "rm -rf dist && tsc"
  },
  "private": false
}
```


## Publish the Package
We can publish our package using `npm publish` command. You could find
more information on this command [here](https://docs.npmjs.com/cli/v8/commands/npm-publish).
In order to ensure published package is always transpiled from TypeScript
before running `npm publish`, we can add additional command to `package.json` to automate
this process. We can add `prepublish` inside scripts array to remove existing `dist` folder 
and transpile and create a new distribution folder.
```json
{
  "scripts": {
    "prepublish": "rm -rf dist && tsc"
  }
}
```


#### Credits
Copyright &copy; 2022. All Rights Reserved.
