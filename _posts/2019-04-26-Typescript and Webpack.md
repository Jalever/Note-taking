---
layout: post
title: Typescript & Webpack
subtitle: Typescript学习笔记系列
date: 2019-04-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Typescript
---

npm packages
```
npm i -D typescript awesome-typescript-loader @types/react @react-dom
```

## 2.create `tsconfig.js`
```json
{
"compilerOptions": {
    "outDir": "./dist/",
    "jsx": "react",
    "sourceMap": true,
    "allowJs": true,
    "target": "es5",
    "module": "es6",
    "noImplicitAny": true
},
"include": ["./src/**/*"]
}
```

## 3.webpack.config.js
```js
...
module: {
    ...
    {
        test: /\.tsx?$/,
        loader: "awesome-typescript-loader"
    },{
        enforce: "pre",
        test:/\.js$/,
        loader: "source-map-loader"
    }
    ...
},
...
resolve: {
    ...
    extensions: ["tsx", "ts", "js"]
}

...
```

## 4.interact with SaSS
at first, create file named `declaration.d.ts` <br/>
and then write down `declare module '*.scss';`


---

## Install our dependencies
```js
npm install --save react react-dom @types/react @types/react-dom
```
That `@types/` prefix means that we also want to get the declaration files for `React` and `React-DOM`.<br/>

Usually when you import a path like "react", it will look inside of the react package itself;<br/>

however, not all packages include declaration files, so `TypeScript` also looks in the `@types/react` package as well.

```git
npm install --save-dev typescript awesome-typescript-loader source-map-loader
```
`awesome-typescript-loader` helps `Webpack` compile your `TypeScript` code using the `TypeScript`’s standard configuration file named `tsconfig.json`. <br/>

`source-map-loader` uses any sourcemap outputs from `TypeScript` to inform `webpack` when generating its own sourcemaps. This will allow you to debug your final output file as if you were debugging your original `TypeScript` source code.

## Add a `TypeScript` configuration file
in `tsconfig.json`
```json
{
    "compilerOptions": {
        "outDir": "./dist/",
        "sourceMap": true,
        "noImplicitAny": true,
        "module": "commonjs",
        "target": "es6",
        "jsx": "react"
    },
    "include": [
        "./src/**/*"
    ]
}
```

## Write some codes
in `./src/componnets/Hello.tsx`
```typescript
import * as React from "react";

export interface HelloProps { compiler: string; framework: string; }

// 'HelloProps' describes the shape of props.
// State is never set so we use the '{}' type.
export class Hello extends React.Component<HelloProps, {}> {
    render() {
        return <h1>Hello from {this.props.compiler} and {this.props.framework}!</h1>;
    }
}
```

in `./src/index.tsx`
```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

import { Hello } from "./components/Hello";

ReactDOM.render(
    <Hello compiler="TypeScript" framework="React" />,
    document.getElementById("example")
);
```

in `./src/index.html`
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>Hello React!</title>
    </head>
    <body>
        <div id="example"></div>

        <!-- Dependencies -->
        <script src="./node_modules/react/umd/react.development.js"></script>
        <script src="./node_modules/react-dom/umd/react-dom.development.js"></script>

        <!-- Main -->
        <script src="./dist/bundle.js"></script>
    </body>
</html>
```


in `webpack.config.js`
```js
module.exports = {
    entry: "./src/index.tsx",
    output: {
        filename: "bundle.js",
        path: __dirname + "/dist"
    },

    // Enable sourcemaps for debugging webpack's output.
    devtool: "source-map",

    resolve: {
        // Add '.ts' and '.tsx' as resolvable extensions.
        extensions: [".ts", ".tsx", ".js", ".json"]
    },

    module: {
        rules: [
            // All files with a '.ts' or '.tsx' extension will be handled by 'awesome-typescript-loader'.
            { test: /\.tsx?$/, loader: "awesome-typescript-loader" },

            // All output '.js' files will have any sourcemaps re-processed by 'source-map-loader'.
            { enforce: "pre", test: /\.js$/, loader: "source-map-loader" }
        ]
    },

    // When importing a module whose path matches one of the following, just
    // assume a corresponding global variable exists and use that instead.
    // This is important because it allows us to avoid bundling all of our
    // dependencies, which allows browsers to cache those libraries between builds.
    externals: {
        "react": "React",
        "react-dom": "ReactDOM"
    }
};
```

## Datatypes in TypeScript
- Number
- String
- Boolean
- Void
- Arrays
- Any
