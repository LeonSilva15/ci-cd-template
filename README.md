# CI/CD Template

## GitHub Action
1. Click on actions
2. Click on new workflow
3. Click on Simple Workflow (configure)
> [GitHub Actions docs](https://docs.github.com/en/actions)

## NPM
Install NVM
Install the latest LTS
```sh
    nvm install --lts
```
> [freeCodeCamp guide](https://www.freecodecamp.org/news/node-version-manager-nvm-install-guide/)

## Init your project
Initialize using npm
```sh
npm init
```
> [NPM init](https://docs.npmjs.com/cli/v6/commands/npm-init)

## Add VSCode configurations
1. Create a `.vscode` folder
2. Add recommended extension
    * Create the extensions file inside the `.vscode` folder
        ```sh
        touch extensions.json
        ```
    * Add your recommended extensions in json format
        ```json
        {
            "recommendations": ["<extension-id>", "<extension-id>", ...]
        }
        ```
> [Guide form Krishna Pravin](https://dev.to/askrishnapravin/recommend-vs-code-extensions-to-your-future-teammates-4gkb)

## ESLint and Prettier
1. Install the ESLint extension
2. Install the Prettier extension
3. Install eslint-config-prettier
    * Turns off all ESLint rules that could conflict with Prettier
        ```sh
        npm install --save-dev eslint-config-prettier
        ```
4. Install eslint-plugin-prettier
    * Integrates the Prettier rules into ESLint rules
        ```sh
        npm install --save-dev eslint-plugin-prettier
        ```
5. Install prettier
    * Adds prettier as a development dependency
        ```sh
        npm install --save-dev --save-exact prettier
        ```
6. Create the .eslint.config.js file and extend prettier
    * Integrates the previous downloaded configs
        ```js
        const eslintConfigPrettier = require("eslint-config-prettier");
        const eslintPluginPrettierRecommended = require("eslint-plugin-prettier/recommended");

        module.exports = [
            // Any other config imports go at the top
            eslintPluginPrettierRecommended,
            eslintConfigPrettier,
        ];
        ```
7. Add the prettier command to your package.json scripts
    * Enable the project to run the command
        ```json
        "prettier-format": "prettier --config .prettierrc '**/*.{js,jsx,ts,tsx}' --write"
        ```
> [ESLint + Prettier guide](https://www.robinwieruch.de/prettier-eslint/)

> [eslint-config-prettier repo](https://github.com/prettier/eslint-config-prettier)

> [eslint-plugin-prettier repo](https://github.com/prettier/eslint-plugin-prettier)

## Husky
1. Install Husky as a development dependency
    ```sh
        npm install --save-dev husky
    ```
2. Initialize Husky (This creates the pre-commit file)
    ```sh
        npx husky init
    ```
> [Husky docs](https://typicode.github.io/husky/)

## Lint Staged
1. Install lint-staged as a development dependency
    ```sh
        npm install -D lint-staged
    ```
2. Add the .lintstagedrc file
    ```sh
        touch .lintstagedrc
    ```
3. Add the config
    ```json
    {
        "**/*.{ts,tsx,js,jsx}": ["eslint --fix", "npm run prettier-format"]
    }
    ```
5. Run lint-staged in the pre-commit
    ```sh
        echo "npx lint-staged" > .husky/pre-commit
    ```
> [lint-staged repo](https://github.com/lint-staged/lint-staged)

## Commit Lint
```sh
npm install --save-dev @commitlint/{cli,config-conventional}
```
* create the config file `commitlint.config.js`
> [commitlint docs](https://commitlint.js.org/guides/getting-started.html)

## Conventional commits
Install the conventional commits config
```sh
npm install --save-dev @commitlint/config-conventional @commitlint/cli
```
Add the conventional commits config to commitlint
```sh
echo "export default {extends: ['@commitlint/config-conventional']};" > commitlint.config.js
```
On .husky create the `commit-msg` file and add
```sh
npx --no -- commitlint --edit $1
```
> [Conventional commits repo](https://github.com/conventional-changelog/commitlint/tree/master/@commitlint/config-conventional)


### Test all the config until now
1. Create a js/ts/jsx/tsx file and add some invalid random text
2. Commit it
    * It should fail the lint-staged check

---
#### In case you need to undo a commit
```sh
git reset --soft HEAD~1 
```

#### Another option of guide:
[Husky + Commit Lint + Lint Staged + ESLint guide](https://medium.com/@nburgueno.dev/eleva-tu-proyecto-c%C3%B3mo-integrar-husky-commitlint-lint-staged-y-eslint-8725cd90e343)