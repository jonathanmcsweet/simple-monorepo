# simple monorepo

A Node.js CLI utility for building simple monorepos with NPM. Currently buggy and experimental...

```sh
npm install simple-monorepo --save-dev
```

## Features

* **Parallel.** Runs package scripts and commands in parallel.

## Motivation

[`https://github.com/mariuslundgard/monorepo`]

[`Other Monorepos`]
Other monorepo tools prescribe forms of linking between repos and installing dependencies that differ from the standard way NPM installs dependencies.

This simple monorepo is intended to simulate, as close as possible, the way NPM will install/consume your repos when they're used as dependencies. It also does this at the expense of speed. Other tools will likely work better for large monorepo instances.

## Usage

Add a `monorepo.json` to the root of the project. Example:

```json
{
  "packages": ["packages/*"]
}
```

#### Install Packages
To install all the sub-package dependencies, run:

```sh
simple-monorepo install
```
#### Link Packages
To link packages together to test interdependent changes.
```sh
simple-monorepo link
```
Excludes a symlink to the actual package receiving the links.

The default behavior for link is to only link to packages/* that are actually present in node_modules after installation. You can override this behavior and force symlinks for all packages, excluding the actual one being given symlinks, by running:

```sh
simple-monorepo link -- --all
```

#### Publish Packages
To publish all the sub-package dependencies, run:

```sh
simple-monorepo publish
```

#### Run Commands
To run a command script in each of the packages, run:

```sh
simple-monorepo run {{command}}
```

## API

### `monorepo(args, flags, opts, cb)`

`simple-monorepo` may be used as a Node.js module:

```js
const monorepo = require('simple-monorepo')

monorepo(
  ['test'],
  {cwd: path.resolve(__dirname, 'path/to/root')},
  err => {
    if (err) {
      console.error(err.message)
      process.exit(err.code || 1)
    }
  }
)
```
