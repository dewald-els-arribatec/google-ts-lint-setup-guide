[![Code Style: Google](https://img.shields.io/badge/code%20style-google-blueviolet.svg)](https://github.com/google/gts)

# TS Linter and Prettier

Sample project using the Google TS Linter.

## Table of Contents

- [TS Linter and Prettier](#ts-linter-and-prettier)
  - [Table of Contents](#table-of-contents)
  - [Description](#description)
  - [Install ESLint and Prettier](#install-eslint-and-prettier)
    - [GTS Prompts](#gts-prompts)
    - [Install TypeScript ESLint Package](#install-typescript-eslint-package)
    - [Update `tsconfig.json`](#update-tsconfigjson)
  - [Important files](#important-files)
  - [WebStorm Configuration](#webstorm-configuration)
    - [WebStorm - ESLint](#webstorm---eslint)
      - [WebStorm - Configuration steps for ESLint](#webstorm---configuration-steps-for-eslint)
    - [WebStorm - Prettier](#webstorm---prettier)
      - [WebStorm Configuration steps for Prettier](#webstorm-configuration-steps-for-prettier)
  - [Visual Studio Code Extensions](#visual-studio-code-extensions)
    - [Extensions](#extensions)
  - [GTS `package.json` Scripts](#gts-packagejson-scripts)
  - [Husky - Pre-commit Hook](#husky---pre-commit-hook)
    - [Setup Husky - Automatic configuration](#setup-husky---automatic-configuration)
    - [Configure Husky Pre-Commit](#configure-husky-pre-commit)
    - [⛔️ Husky - Remove auto generated folders](#️-husky---remove-auto-generated-folders)
    - [Additional remarks](#additional-remarks)
    - [Known Extensions](#known-extensions)

## Description

Setup a project to use the [Google TypeScript Linter and Prettier](https://github.com/google/gts)

## Install ESLint and Prettier

Run the following command from the root directory of the project and follow the prompts.

```shell
npx gts init
# Initialize Google TypeScript Library
```

> 📝 If you are prompted to install `create-gts`, enter Yes.

The above command will install the `gts` package and create the necessary files to lint and format the project.

### GTS Prompts

- Overwrite devDependency for `TypeScript`: **NO**
- Overwrite devDependency for `@types/node`: **NO**
- Overwrite `package.json` already has a script for `lint`: **YES**
- `./tsconfig.json` already exists, Overwrite: **NO**
- `./.eslintrc.json` already exists, Overwrite: **YES**

### Install TypeScript ESLint Package

Install the latest TypeScript ESLint package.

```sh
npm i @typescript-eslint/eslint-plugin@latest -D
```

### Update `tsconfig.json`

Add the following line at the start of the `.tsconfig.json` file to your project.

```javascript
{
  "extends": "./node_modules/gts/tsconfig-google.json",
  "compilerOptions": {
    ...
  }
  ... // Rest of the configuration
}

```

> 📝 NOTE: Replace the `extends` property if it already exists.

## Important files

```text
.
├── .editorconfig           # Configuration for code editor
├── .eslintignore           # Folders to ignore for linting
├── .eslint.json            # Linting Rules that inherit node_modules/gts/.eslint.json
├── .prettier.js            # Formatting that inherits node_modules/gts/.prettier.json
└── ...                     # Other project files and folders
```

## WebStorm Configuration

For [WebStorm](https://www.jetbrains.com/webstorm/) users some addition configuration is required.

### WebStorm - ESLint

Open Preferences from `File > Preferences` and search for "eslint".

#### WebStorm - Configuration steps for ESLint

1. Select the "Automatic ESLint configuration" option
2. _[Optionally]_ Check the "Run eslint --fix" on save.

![Enable ESlint](./img/webstorm-eslint.png)

> 📖 More information can be found in the [JetBrains Documentation on ESLint for WebStorm](https://www.jetbrains.com/help/webstorm/eslint.html).

### WebStorm - Prettier

Open Preferences from `File > Preferences` and Search for "prettier".

#### WebStorm Configuration steps for Prettier

1. From the dropdown, select the prettier folder from the `node_modules` folder for the current project.
   1. Leave the **"run for files"** as its default value
2. Check the **"On 'Reformat Code' action"** checkbox
3. _[Optionally]_ Check the **"On Save"** checkbox

![Enable Prettier](./img/prettier-settings.png)

> 📖 More information can be found in the [Prettier documentation](https://prettier.io/docs/en/webstorm.html#jetbrains-ides-webstorm-intellij-idea-pycharm-etc)

## Visual Studio Code Extensions

Ensure the below extensions are installed when using [Visual Studio Code](https://code.visualstudio.com/).

### Extensions

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## GTS `package.json` Scripts

```javascript
{
  ...
  "scripts": {
    ...
    "fix": "gts fix", // Automatically tries to fix linting and formatting
    "lint": "gts lint", // Lints and checks the formatting and report via terminal
    "clean": "gts clean", // Removes output files
  }
}
```

The above commands are added by the `gts` package.

## Husky - Pre-commit Hook

[Husky](https://typicode.github.io/husky/#/?id=automatic-recommended) is used to easily configure a [Git `pre-commit`](https://git-scm.com/docs/githooks#_pre_commit) to lint, format and/or test your code before it is committed to `git`.

> ℹ️ This will mean your code can not be committed until the linting issues have been resolved.

### Setup Husky - Automatic configuration

Run the following command in the root directory of the project.

```sh
npx husky-init && npm install
# Install and auto configure Husky
```

The above command will create a `.husky` folder and a `pre-commit` file. In the pre-commit file, a `npm` command can be configured to run before code can be committed to git. Also see Husky's [generated files](#️-husky---remove-auto-generated-folders) section.

> 📝 Multiple `npm` scripts may be added.

### Configure Husky Pre-Commit

The Husky Pre-commit file will be automatically generated and can be found in the `.husky` folder.

```sh
# File: .husky/pre-commit

#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

# Execute gts fix script from package.json.
npm run fix

# Add additional scripts you want to run BEFORE commit e.g. npm test
```

### ⛔️ Husky - Remove auto generated folders

Husky will generate a `./src` folder if none is detected in the initialization step. Remove this folder before committing. NextJS Projects are an example of this, since it does not contain a `src` folder.

### Additional remarks

Some VS Code extension cause conflicts with ESLint and must be disabled for the GTS Linter to work effectively.

### Known Extensions

- [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
