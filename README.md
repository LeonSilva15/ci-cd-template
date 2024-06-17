# CI/CD Template

## GitHub Action
GitHub Actions is a powerful CI/CD (Continuous Integration and Continuous Deployment) automation tool that allows you to automate workflows directly from your GitHub repository. With GitHub Actions, you can build, test, and deploy your code on different platforms, ensuring that your software remains in a constant state of readiness for release.
### Create a simple GitHub Action from your repo:
1. Click on actions
2. Click on new workflow
3. Click on Simple Workflow (configure)
> [GitHub Actions docs](https://docs.github.com/en/actions)

## NPM
NPM (Node Package Manager) is a widely used package manager for JavaScript, specifically for Node.js. It facilitates the installation, sharing, and management of code packages, making it easier for developers to manage project dependencies and collaborate with others.

### NVM
NVM (Node Version Manager) is a powerful tool designed to manage multiple versions of Node.js on a single machine. It allows developers to switch between different versions of Node.js effortlessly, which is particularly useful when working on multiple projects with varying Node.js requirements.

**Install npm through nvm:**
> [freeCodeCamp guide](https://www.freecodecamp.org/news/node-version-manager-nvm-install-guide/)

**Install the latest LTS**
```sh
nvm install --lts
```

## Init your project
The npm init command is used to create a new package.json file for your Node.js project. The package.json file is essential for managing a project's metadata, dependencies, scripts, and various configurations. This command helps streamline the setup of a new project by guiding you through a series of questions to generate this file.
Initialize using `npm`
```sh
npm init
```
> [NPM init](https://docs.npmjs.com/cli/v6/commands/npm-init)

## Add VSCode configurations
Workspace configurations help you customize settings, tasks, and launch configurations specifically for your project, ensuring a consistent development environment across team members.
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
ESLint and Prettier are two essential tools in modern JavaScript development that help maintain code quality and consistency. While they serve different purposes, they often work together to ensure your codebase is clean, readable, and adheres to best practices.

### ESLint
ESLint is a static code analysis tool used to identify and fix problems in JavaScript code. It helps enforce coding standards and catch common programming errors before they become issues.

### Prettier
Prettier is an opinionated code formatter that enforces a consistent style by parsing your code and reprinting it with its own rules. Unlike linters, which focus on finding and reporting issues, Prettier focuses on formatting your code.

### Installation
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
Husky is a tool for managing Git hooks in a project. Git hooks are scripts that run automatically at specific points in the Git workflow, such as before a commit is created or before a push is made. Husky simplifies the setup and management of these hooks, allowing developers to automate tasks such as running tests, linting code, or formatting files before changes are committed.
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
Lint Staged is a tool that allows you to run linters on your staged files, i.e., files that are added to the staging area in Git (usually with git add) before committing. This ensures that only the files you are about to commit are checked, making the linting process faster and more efficient, and ensuring that your code meets quality standards before it enters your version control system.
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
CommitLint is a tool that helps enforce consistent commit message conventions in your project. By validating commit messages based on predefined rules, CommitLint ensures that your commit history is readable, informative, and easy to understand. This is particularly useful in larger projects and teams where maintaining a clear and consistent commit history is important for collaboration and code management.
```sh
npm install --save-dev @commitlint/{cli,config-conventional}
```
* create the config file `commitlint.config.js`
> [commitlint docs](https://commitlint.js.org/guides/getting-started.html)

## Conventional commits
Conventional Commits is a standardized commit message convention that provides a consistent way to structure commit messages. This convention makes commit histories more readable, and facilitates automated tools for versioning, release notes, and changelogs. By following the Conventional Commits specification, teams can ensure that their commit messages are informative and structured.
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