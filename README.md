# Getting Started with Creating a React Component Library

## Introduction

This tutorial will guide you through the process of creating and publishing your own custom React component library and hosting it on GitHub.

By the end of this tutorial, you will be able to do the following in all of your future React projects:

```bash
npm install @my-github-account/my-cool-component-library

import MyCustomComponent from '@my-github-account/my-cool-component-library';

const MyApp = () => {
  return (
    <div>
      <MyCustomComponent />
    </div>
  );
};
```
## Prerequisites and Setup
This project assumes you are familiar with and have installed:

 >Code editor / IDE (this tutorial uses VS Code but any IDE will work)
 >NPM (NPM is installed when you install Node.js on your machine)
 >Installing packages (presume you know how to add packages to a JavaScript project with npm install)
 >Bash terminal (or another terminal you are comfortable with for running commands)
 >Git (we will be creating a Git repository on our machine and publishing it to GitHub, though all instructions will be provided on how to follow along)
 >React (how to create simple components using JSX)
 >TypeScript (how to create an object interface with simple properties)


## Initialize Your Project
First, we will initialize our project.

```bash
npm init
```
You can take the defaults for all the values; we'll edit them later in the tutorial.

Next, we will add the tools necessary to create our components.
```bash
npm install react typescript @types/react --save-dev
```
## Creating Components
Now we can create our first component. Because we are creating a library, we are going to create index files for each tier and export our components from each one to make it as easy as possible for the people using our library to import them.

Within the root of your project, create the following file structure:
###### .
###### ├── src
###### │   ├── components
###### │   │   ├── Button
###### │   │   │   ├── Button.tsx
###### │   │   │   └── index.ts
###### │   │   └── index.ts
###### │   └── index.ts
###### ├── package.json
###### └── package-lock.json
Make sure to double-check your structure. You should have three index.ts files and a Button.tsx file inside a Button directory. If you have a preferred way of structuring React components within a project, you are of course welcome to do it however you like, but this is the structure we will follow for this tutorial.

## Creating Button.tsx
Begin by creating Button.tsx:
```bash
// src/components/Button/Button.tsx
import React from "react";

export interface ButtonProps {
  label: string;
}

const Button = (props: ButtonProps) => {
  return <button>{props.label}</button>;
};

export default Button;
```
To keep things simple, we will just export a button that takes a single prop called label. We can add more complexity and styles to our components once we have confirmed that our basic template is set up correctly.

## Updating Index Files
After our button, we update the index file inside our Button directory:
```bash
// src/components/Button/index.ts
export { default } from "./Button";
```
Then we export that button from the components directory:
```bash
// src/components/index.ts
export { default as Button } from "./Button";
```
And finally, we will export all of our components from the base src directory:
```bash 
// src/index.ts
export * from './components';
```
## Adding TypeScript
Up until now, we haven't yet initialized TypeScript in our project. Although you technically don't need a configuration file to use TypeScript, for the complexity of building a library, we are definitely going to need one.

You can initialize a default configuration by running the following command:
```bash
npx tsc --init
```
That will create a tsconfig.json file for us in the root of our project that contains all the default configuration options for TypeScript.

If you would like to learn more about the many options in a tsconfig.json file, modern versions of TypeScript will automatically create descriptive comments for each value. In addition, you can find full documentation on the configuration here.

You may notice, depending on your IDE, that immediately after initializing, you begin to get errors in your project. There are two reasons for that: the first is that TypeScript isn't configured to understand React by default, and the second is that we haven't defined our method for handling modules yet, so it may not understand how to manage all of our exports.

To fix this, we are going to add the following values to tsconfig.json:
```bash
{
  "compilerOptions": {
    // Default
    "target": "es5",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true,

    // Added
    "jsx": "react",
    "module": "ESNext",
    "declaration": true,
    "declarationDir": "types",
    "sourceMap": true,
    "outDir": "dist",
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "emitDeclarationOnly": true
  }
}
```
I have separated these values into a couple of different sections based on the default tsconfig.json created using the most recent version of TypeScript as of this writing (4.4). The values commented as default should already be set for you by default (you will want to double-check and make sure, however).

The values marked added are new values that we need for our project. We'll briefly outline why we need them:

"jsx": "react" -- Transform JSX into React code
"module": "ESNext" -- Generate modern JS modules for our library
"declaration": true -- Output a .d.ts file for our library types
"declarationDir": "types" -- Where to place the .d.ts files
"sourceMap": true -- Mapping JS code back to its TS file origins for debugging
"outDir": "dist" -- Directory where the project will be generated
"moduleResolution": "node" -- Follow node.js rules for finding modules
"allowSyntheticDefaultImports": true -- Assumes default exports if none are created manually
"emitDeclarationOnly": true -- Don't generate JS (Rollup will do that) only export type declarations
Once you add those values to your TS configuration file, you should see the errors in Button.tsx and other files immediately disappear.






