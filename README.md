<div align="center">
    <h1>eslint-plugin-json-format</h1>
    <a href="https://circleci.com/gh/Bkucera/eslint-plugin-json-format"><img alt="CircleCI" src="https://img.shields.io/circleci/build/gh/Bkucera/eslint-plugin-json-format"></a>
    <br>
    <a href="https://www.npmjs.com/package/eslint-plugin-json-format"><img src="https://img.shields.io/npm/v/eslint-plugin-json-format.svg?style=flat"></a>
    <a href="https://www.npmjs.com/package/eslint-plugin-json-format"><img src="https://img.shields.io/npm/dm/eslint-plugin-json-format.svg"></a>
    <a href="https://github.com/bkucera/eslint-plugin-json-format/blob/master/LICENSE"><img src="https://img.shields.io/github/license/bkucera/eslint-plugin-json-format.svg"></a>
    


</div>
Lint and auto-fix your `json` with `eslint`

## Features

- lint and auto-fix `json` files (files ending with `.json` or `rc`)
- auto-sort `package.json` files (default `true`, can be disabled and sorting configured)
- ignores `json-with-comments` files (default `["**/.tsconfig.json", ".vscode/**"]`)
- ignores certain files by default (default `["**/package-lock.json"]`)

## Installation

You'll first need to install [ESLint](http://eslint.org):

```sh
npm i eslint --save-dev
```

Next, install `eslint-plugin-json-format`:

```sh
npm install eslint-plugin-json-format --save-dev
```

## Usage

Add `json-format` to the plugins section of your `.eslintrc` configuration file. You can omit the `eslint-plugin-` prefix:

```json
{
  "plugins": [
    "json-format"
  ]
}
```

**cli example**:
```sh
# lint entire poject for js and various json files
eslint --ext .js,.json,.eslintrc,.babelrc --fix .
```

> Note: **In order to lint hidden files** (e.g. `.eslintrc`, `.babelrc`), you'll need to modify/create a `.eslintignore` in your project root with these contents:
`.eslintignore`:
```gitignore
# eslint ignores hidden files by default
!.*
```

## Configuration

### default configuration** (`.eslintrc`):
```json
"settings": {
  "json/sort-package-json": true,
  "json/ignore-files": ["**/package-lock.json"],
  "json/json-with-comments-files": ["**/tsconfig.json", ".vscode/**"],
  "json/package-json-sort-order": [
      "name",
      "version",
      "description",
      "private",
      "main",
      "browser",
      "scripts",
      "husky",
      "dependencies",
      "devDependencies",
      "peerDependencies",
      "files",
      "bin",
      "engines",
      "types",
      "typings",
      "productName",
      "license",
      "repository",
      "homepage",
      "author",
      "bugs",
    ]
}
```
> Note: glob patterns use [`minimatch`](https://github.com/isaacs/minimatch/) against pathnames relative to the project root (cwd)

### examples:

to turn off `sort-package-json` for example, in your `.eslintrc`:
```json
{
  "plugins": [
    "json-format"
  ],
  "settings": {
    "json/sort-package-json": false,
  }
}
```

to format `tsconfig.json` (this will strip comments!), in your `.eslintrc`:
```json
{
  "plugins": [
    "json-format"
  ],
  "settings": {
    "json/json-with-comments-files": [],
  }
}
```

change the sort order of `package.json`:
```json
{
  "plugins": [
    "json-format"
  ],
  "settings": {
    "json/package-json-sort-order": ["license", "dependencies"],
  }
}
```

## Editor Configuration

**VSCode**:

In order for editor integration via the [`vscode-eslint`](https://github.com/microsoft/vscode-eslint) extension, you'll need to enable linting `json` files.

`settings.json`:
```json
// enable eslint fix-on-save
  "eslint.autoFixOnSave": true,
  "eslint.validate": [
    {
      "language": "json",
      "autoFix": true
    },
```

> to auto-format `json-with-comments-files`, also add `"language": "jsonc"`

## License
[MIT](/LICENSE.md)

## Credits

large amount of code borrowed from [`eslint-plugin-html`](https://github.com/BenoitZugmeyer/eslint-plugin-html)
