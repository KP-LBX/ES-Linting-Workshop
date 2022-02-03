# ES-Linting-Workshop
Workshop to show how to use ESLint in JS projects.

## Project Setup 
```
git clone git@github.com:KP-LBX/ES-Linting-Workshop.git
cd ES-Linting-Workshop
$ npm init -y
```

## ESLint Setup
```
$ npm install eslint --save-dev
$ npx eslint --init
```
The first prompt will be:
```
? How would you like to use ESLint? …
  To check syntax only
  To check syntax and find problems
```

Choose the To check syntax, find problems, and enforce code style option.

The next prompt will be:
```
 What type of modules does your project use? …
 ❯ JavaScript modules (import/export)
  CommonJS (require/exports)
  None of these
 ```


The next prompt will say:

```
? Which framework does your project use? …
  React
  Vue.js
❯ None of these
```
Choose the None of these option.

The next prompt will ask:
```
? Does your project use TypeScript? › No / Yes
```
Choose the No option.

The following prompt will say:
```
? Where does your code run? …  (Press <space> to select, <a> to toggle all, <i> to invert selection)
✔ Browser
  Node
```
Choose the Browser option.

The next prompt will say:
```
✔ How would you like to define a style for your project? …
❯ Use a popular style guide
  Answer questions about your style
  Inspect your JavaScript file(s)
```
Choose the Use a popular style guide option.

For the Which style guide do you want to follow? prompt, choose the Airbnb: https://github.com/airbnb/javascript option.

The next prompt will ask:
```
? What format do you want your config file to be in? …
  JavaScript
  YAML
❯ JSON
```
Choose the JSON option.

You will then see this message:
```
Checking peerDependencies of eslint-config-airbnb-base@latest
The config that you've selected requires the following dependencies:

eslint-config-airbnb-base@latest eslint@^5.16.0 || ^6.8.0 || ^7.2.0 eslint-plugin-import@^2.21.2
```

The last prompt will ask:
```
? Would you like to install them now with npm? › No / Yes
```
Choose Yes option.

Now you have your .eslintrc setup.


## Run ES Linter
```
$ npx eslint src/*.js
```

## Run ES Linter Fix
```
$ npx eslint src/*.js --fix
```

## Setup Prettier
```
npm i prettier eslint-config-prettier eslint-plugin-prettier -D
```
Add prettier plugin to eslintrc file.
```
'extends': [ 'airbnb', "plugin:prettier/recommended" ]

add eslint to package.json 

```
$ npm run lint 'src/*.js' 
```
```



## ES LINTING
A linter is a static code analysis tool that often flags your code about:
* out of the/your code standards
* misusages of language features that are obsolete or harmful
* misusages of programming in general
* non-consistent structure of code


The first parameters could be a number from 0 to 2:
* 0 – Turn the rule off
* 1 – Turn the rule on as a warning
* 2 – Turn the rule on as an error


module.exports = {
  rules: {
    // enable additional rules
    quotes: ["error", "double"],
    semi: ["error", "always"]
  }
};


example https://github.com/eslint/eslint/blob/main/conf/eslint-recommended.js

## Extends
Instead of manually configuring each rule individually, you can apply a bulk rule configuration from a shared config.
The extends property in .eslintrc allows extending off a set of rule configurations from an existing configuration.
For example, extending off the base ESLint eslint:recommended configuration will enable a subset of core rules that report common problems.

Shared configs are distributed as eslint-config-* NPM packages. One of the commonly used configurations is Airbnb's eslint-config-airbnb.

ESlint Docs: Extending Configuration Files


ESLint extends configurations recursively, so a shared eslint-config-* configuration can also have its own extends, env,plugins,parser properties which will apply to the.eslintrc configuration.
Many recommended base configurations shared from eslint-config-* already set the parser, plugins, and env properties.
There is no need to re-declare these properties in your own .eslintrc if you're extending off a recommended base configuration that already has these declared.


## Plugins
The plugins property in .eslintrc allows using third-party plugins to apply specific linting rules for different code bases.
For example, eslint-plugin-react, and eslint-plugin-vue, adds specific linting rules for React or Vue projects, respectively.
ESLint plugins contain implementation for additional rules that ESLint will check for, however, these defined ESlint rules still need to be manually configured in an .eslintrc to determine how to handle each rule.
The new rules defined by an eslint-plugin-* still need to be configured under the rules property, or by taking a set of rule configurations in the extends property.
ESlint Docs: Configuring Plugins
.eslintrc.js
// The example settings below tell ESLint use the eslint-plugin-react linting rules, and manually configures two rules.
```
module.exports = {
  plugins: ["react"],
  parserOptions: {
    ecmaFeatures: {
      jsx: true
    }
  },
  rules: {
    "react/jsx-uses-react": "error",
    "react/jsx-uses-vars": "error"
  }
};
```


## Environment
The env property in .eslintrc declares which environments your code is expected to run in.
Each environment brings with it a certain set of predefined global variables, and prevents ESLint from throwing an no-undef rule error when referencing an expected global variable such as, window, or document.
ESlint Docs: Specifying Environments
.eslintrc.js
// The example settings below tell ESLint to enable browser and node global variables like `window`.
```
module.exports = {
  env: {
    browser: true,
    node: true
  }
};
```
## Parser
The parser property in .eslintrc declares which parser ESLint should use to parse your code into an AST. By default, ESLint uses Espree as its parser.

ESlint Docs: Specifying Parser

.eslintrc.js
// The example settings below tell ESLint to use the TypeScript ESTree parser.
```
module.exports = {
  parser: "@typescript-eslint/parser"
};
```

## Parser Options
The parserOptions property in .eslintrc specifies the JavaScript language options you want to support.

By default, ESLint supports ECMAScript 5 syntax. Configure parserOptions to enable support for other ECMAScript versions as well as JSX.

ESlint Docs: Specifying Parser Options

.eslintrc.js
// The example settings below specifies ESLint to enable support for ECMAScript 2018 and JSX.
```
module.exports = {
  parserOptions: {
    ecmaVersion: 2018,
    ecmaFeatures: {
      jsx: true
    }
  }
};
```

## React
From the eslint-plugin-react docs, we need a minimum config specifying:
```
.eslintrc.js
module.exports = {
  plugins: ["react"], // use the plugin rules within ESLint
  parserOptions: {
    ecmaFeatures: {
      jsx: true // enable JSX support
    }
  },
  settings: {
    react: {
      pragma: "React", // Pragma to use, default to "React"
      version: "detect" // React version
    }
  }
};
```

## TypeScript
From the @typescript-eslint/eslint-plugin docs, we need a minimum config specifying:
```
.eslintrc.js
module.exports = {
  parser: "@typescript-eslint/parser", // allows ESLint to understand TypeScript
  plugins: ["@typescript-eslint"] // use the plugin rules within ESLint
};
```


## TypeScript: plugin:@typescript-eslint/recommended
@typescript-eslint/eslint-plugin comes with a bundled recommended base config.
```
.eslintrc.js
module.exports = {
  // Remove these config
- parser: "@typescript-eslint/parser",
- plugins: ["@typescript-eslint"],

  // Add these config
+ extends: [
+   "eslint:recommended", // ESLint's inbuilt "recommended" config
+   "plugin:@typescript-eslint/eslint-recommended",
+   "plugin:@typescript-eslint/recommended"
+ ]
};
```

## React: plugin:react/recommended
eslint-plugin-react comes with a bundled recommended base config.
```
.eslintrc.js
module.exports = {
  // Remove these config
- plugins: ["react"],
- parserOptions: {
-   ecmaFeatures: {
-     jsx: true
-   }
- },

  // Add these config
+ extends: [
+   "eslint:recommended",
+   "plugin:react/recommended"
+ ],
  settings: {
    react: {
      pragma: "React",
      version: "detect"
    }
  }
};

```




## Sample JS To Be Fixed
```
const name = 'James'

const person = {first: name}

console.log(person)

const sayHelloLinting = (fName) => {
console.log(`Hello linting, ${fName}`);
};


// bad
var count = 1;
if (true) {
  count += 1;
}

// const and let only exist in the blocks they are defined in.
{
    let a = 1;
    const b = 1;
    var c = 1;
  }
  console.log(a); // ReferenceError
  console.log(b); // ReferenceError
  console.log(c); // Prints 1


  // bad
const item = new Object();


function getKey(k) {
    return `a key named ${k}`;
  }
  
  // bad
  const obj = {
    id: 5,
    name: 'San Francisco',
  };
  obj[getKey('enabled')] = true;


  // bad
const atom = {
    value: 1,
  
    addValue: function (value) {
      return atom.value + value;
    },
  };


  const lukeSkywalker = 'Luke Skywalker';


  // bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};
```
