# Create Node project

### Preparation

Install:

- [Code editor](https://code.visualstudio.com/)
- [Nodejs v16.19.0 LTS version](https://nodejs.org/en/). To get v16.19.0 use [nvm](https://github.com/nvm-sh/nvm)
- [Git](https://git-scm.com/)

1. Set vscode extensions (just copy/paste all rows below in search bar):

```
dbaeumer.vscode-eslint
esbenp.prettier-vscode
rangav.vscode-thunder-client
richie5um2.vscode-sort-json
rohit-gohri.format-code-action
streetsidesoftware.code-spell-checker
yzhang.markdown-all-in-one
mhutchie.git-graph
```

2. Set vscode settings:

```
{
  // Runs Prettier, then ESLint
  "editor.codeActionsOnSave": ["source.formatDocument", "source.fixAll.eslint"],
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": false,
  "editor.tabSize": 2,
  "window.zoomLevel": 2,
  "workbench.colorTheme": "Default Dark+"
}
```

3. Create a new repository on GitHub (then you can clone repo or 4-5 steps)
4. `git init`
5. `git remote add origin https://github.com/username/reponame.git`
6. `npm init`
7. `npm i -D eslint prettier eslint-config-prettier`
8. Add to `package.json` file:

```
"main": "src/index.js",
"type": "module",
"scripts": {
    "lint": "npx eslint src",
    "lint:fix": "npm run lint -- --fix",
    "prettier": "npx prettier src --check",
    "prettier:fix": "npm run prettier -- --write",
    "format": "npm run prettier:fix && npm run lint:fix"
  }
```

9. Add files:

#### .prettierrc

```
{}
```

#### .eslintrc

```
{
  "env": {
    "node": true
  },
  "extends": ["eslint:recommended", "prettier"],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "plugins": ["simple-import-sort", "import"],
  "rules": {
    "simple-import-sort/imports": "error",
    "simple-import-sort/exports": "error",
    "import/first": "error",
    "import/newline-after-import": "error",
    "import/no-duplicates": "error"
  },
  "overrides": [
    // override "simple-import-sort" config
    {
      "files": ["*.js", "*.jsx", "*.ts", "*.tsx"],
      "rules": {
        "simple-import-sort/imports": [
          "error",
          {
            "groups": [
              // Packages `react` related packages come first.
              ["^react", "^@?\\w"],
              // Side effect imports.
              ["^\\u0000"],
              // Internal packages.
              ["^(@|components)(/.*|$)"],
              // Parent imports. Put `..` last.
              ["^\\.\\.(?!/?$)", "^\\.\\./?$"],
              // Other relative imports. Put same-folder imports and `.` last.
              ["^\\./(?=.*/)(?!/?$)", "^\\.(?!/?$)", "^\\./?$"],
              // Style imports.
              ["^.+\\.?(css)$"]
            ]
          }
        ]
      }
    }
  ]
}
```

#### .gitignore

```
node_modules/
```

#### src/index.js

```
console.log('Hello world..');
```

10. `npm install -g nodemon`
11. `nodemon src/index.js`
12. You should see `Hello world..` in terminal
13. `git add .`
14. `git commit -m 'feat(*): initial commit'`
15. `git push -u origin master`
