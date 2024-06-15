# CI/CD Template

GitHub Action:
    * click on actions
    * click on new workflow
    * click on Simple Workflow (configure)

NPM:
    * Install the latest LTS
        nvm install --lts

Init your project
    * Initialize using npm
    npm init

Add VSCode configurations
    * Create a .vscode folder

Add recommended extension
    * Create the extensions file inside the .vscode folder
        touch extensions.json
    * Add your recommended extensions in json format
```json
{
    "recommendations": ["<extension-id>", "<extension-id>", ...]
}
```

ESLint and Prettier
    * Install the ESLint extension
    * Install the Prettier extension
    * Install eslint-config-prettier
        ** Turns off all ESLint rules that could conflict with Prettier
        npm install --save-dev eslint-config-prettier
    * Install eslint-plugin-prettier
        ** ntegrates the Prettier rules into ESLint rules
        npm install --save-dev eslint-plugin-prettier
    * Install prettier
        npm install --save-dev --save-exact prettier
        
    * Create the .eslint.config.js file and extend prettier
```js
const eslintConfigPrettier = require("eslint-config-prettier");
const eslintPluginPrettierRecommended = require("eslint-plugin-prettier/recommended");

module.exports = [
    // Any other config imports go at the top
    eslintPluginPrettierRecommended,
    eslintConfigPrettier,
];
```
* Add the prettier command to your package.json scripts
```json
"prettier-format": "prettier --config .prettierrc '**/*.{js,jsx,ts,tsx}' --write"
```

Husky
    * Install Husky as a development dependency
        npm install --save-dev husky
    * Initialize Husky (This creates the pre-commit file)
        npx husky init

Lint Staged
    * Install lint-staged as a development dependency
        npm install -D lint-staged
    * Add the .lintstagedrc file
        touch .lintstagedrc
    * Add the config
```json
{
    "**/*.{ts,tsx,js,jsx}": ["eslint --fix", "npm run prettier-format"]
}
```
    * Run lint-staged in the pre-commit
        echo "npx lint-staged" > .husky/pre-commit

Add commitlint
```sh
npm install --save-dev @commitlint/{cli,config-conventional}
```
create the config file
commitlint.config.js


Add Conventional commits
https://github.com/conventional-changelog/commitlint/tree/master/@commitlint/config-conventional

npm install --save-dev @commitlint/config-conventional @commitlint/cli
echo "export default {extends: ['@commitlint/config-conventional']};" > commitlint.config.js

on .husky creaet the commit-msg file and add
npx --no -- commitlint --edit $1


Test all the config until now
    * Create a js/ts/jsx/tsx file and add some invalid random text
    * Commit it
        ** It should fail the lint-staged check

In case you need to undo a commit:
git reset --soft HEAD~1 