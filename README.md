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
.
### ├── src
### │   ├── components
### │   │   ├── Button
### │   │   │   ├── Button.tsx
### │   │   │   └── index.ts
### │   │   └── index.ts
### │   └── index.ts
### ├── package.json
### └── package-lock.json






