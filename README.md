[![Code Style: Google](https://img.shields.io/badge/code%20style-google-blueviolet.svg)](https://github.com/google/gts)

# TS Linter and Prettier

Sample project using the Google TS Linter.

## Table of Contents

- [TS Linter and Prettier](#ts-linter-and-prettier)
  - [Table of Contents](#table-of-contents)
  - [Description](#description)
  - [Setup ESLint](#setup-eslint)
    - [Update `tsconfig.json`](#update-tsconfigjson)
  - [Important files](#important-files)
  - [WebStorm Configuration](#webstorm-configuration)
    - [WebStorm - ESLint](#webstorm---eslint)
      - [WebStorm Configuration steps for ESLint](#webstorm-configuration-steps-for-eslint)
    - [WebStorm - Prettier](#webstorm---prettier)
      - [WebStorm Configuration Steps for Prettier:](#webstorm-configuration-steps-for-prettier)
  - [Visual Studio Code Extensions](#visual-studio-code-extensions)
    - [Extensions](#extensions)
  - [Package.json Scripts](#packagejson-scripts)
  - [Husky [WIP]](#husky-wip)
    - [Setup Husky](#setup-husky)
    - [Configure Husky Pre-Commit](#configure-husky-pre-commit)
  - [Debugging](#debugging)
  - [TLDR;](#tldr)
    - [Step 1](#step-1)
    - [Step 2](#step-2)
    - [Step 3](#step-3)
      - [TLDR; Configure Webstorm](#tldr-configure-webstorm)
      - [TLDR; Configure VSCode](#tldr-configure-vscode)
    - [Step 4](#step-4)
    - [Step 5:](#step-5)

> ⭐️ Just want the commands? Head over to the [TLDR;](#tldr).

## Description

Setup a project to use the [Google TypeScript Linter and Prettier](https://github.com/google/gts)

## Setup ESLint

Please check the [NOTE on tsconfig.json](#note-on-tsconfigjson).

Run the following command from the root of the project directory and follow the prompts.

```shell
npx gts init
# Initialize Google TypeScript Library
```

The above command will install the `gts` package and create the necessary files to lint and format the project.

> ### Note on tsconfig.json
>
> ## ⛔️ NB: **DO NOT** SELECT YES TO OVERWRITE `tsconfig.json`
>
> &nbsp;

### Update `tsconfig.json`

Add the following line at the start of the `.eslintrc.json` file to your project.

```json
{
  "extends": "./node_modules/gts/tsconfig-google.json",
  ... // Rest of the configuration
}

```

> 📝 NOTE: Replace the `extends` property if it already exists.

## Important files

```
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

#### WebStorm Configuration steps for ESLint

1. Select the "Automatic ESLint configuration" option
2. _[Optionally]_ Check the "Run eslint --fix" on save.

![Enable ESlint](./img/webstorm-eslint.png)

> 📖 More information can be found in the [JetBrains Documentation on ESLint for WebStorm](https://www.jetbrains.com/help/webstorm/eslint.html).

### WebStorm - Prettier

Open Preferences from `File > Preferences` and Search for "prettier".

#### WebStorm Configuration Steps for Prettier:

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

## Package.json Scripts

```json
{
  ...
  "scripts": {
    ...
    "fix": "gts fix", # Automatically tries to fix linting and formatting
    "lint": "gts lint", # Lints and checks the formatting and report via terminal
    "clean": "gts clean", # Removes output files
  }
}
```

The above commands are added by the `gts` package.

## Husky [WIP]

[Husky](https://typicode.github.io/husky/#/) is used to configure `pre-commit` to lint your code before it is committed to git. This will mean your code can not be committed until the linting issues have been resolved.

### Setup Husky

Run the following command in the root of the project being set up.

```sh
npx husky-init && npm install
# Install and configure Husky
```

The above command will create a `.husky` folder and a `pre-commit` file. In the pre-commit file, an npm command can be configured to run before code can be committed to git.

### Configure Husky Pre-Commit

The Husky Pre-commit file will be automatically generated and can be found in the .husky folder.

```sh
# File: .husky/pre-commit

#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

# Execute gts fix script from package.json.
npm run fix
```

## Debugging

Some projects might require an additional installation:

```sh
npm i @typescript-eslint/eslint-plugin@latest -D
```

---

## TLDR;

Too lazy to read. Here are the steps.

### Step 1

**⛔️ DO NOT Say YES to overwrite `tsconfig.json`**

```sh
npx gts init
```

### Step 2

Add the following line at the start of the `.eslintrc.json` file to your project.

```json
{
  "extends": "./node_modules/gts/tsconfig-google.json",
  ... // Rest of the configuration
}

```

### Step 3

#### TLDR; Configure Webstorm

- ESLint
  - Enable Automatic ESLint configuration
- Prettier:
  - Select the prettier folder from the `node_modules` folder for the current project.
  - Check the **"On 'Reformat Code' action"** checkbox

#### TLDR; Configure VSCode

Install ESLint and Prettier [extensions](#extensions)

### Step 4

Run the following command in the root of the project being set up.

```sh
npx husky-init && npm install
# Install and configure Husky
```

Edit the `.husky/pre-commit` file:

File: .husky/pre-commit

```sh
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

# Execute gts fix script from package.json.
npm run fix
# Add more scripts that you want to run BEFORE commit.
```

### Step 5:

Install the typescript linter

```sh
npm i @typescript-eslint/eslint-plugin@latest -D
```

---
