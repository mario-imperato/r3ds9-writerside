# NG Schematics project setup

The schematics cli has to be installed with the command `npm install -g @angular-devkit/schematics-cli` if not already present.
Next the project has been created with the cli by issuing.

```
schematics blank --name=r3ds9-schematics
```

This creates a subdirectory with the stuff.

- Execute `npm install` to install dependencies.
- Add support and helpers with `npm i --save @schematics/angular`
- Add support for the [diff package](https://www.npmjs.com/package/diff) with the two commands:

```
npm i diff
npm i @types/diff --save-dev
```

For dev purposes, create a script in the `package.json` that could look like this: `"build:watch": "tsc -p tsconfig.json --watch",`. In this way a modification
will trigger the rebuild.

In JetBrains create a new `Run >> Edit Configurations...` selezionando npm e scegliendo per lo script il `build:watch` appena creato.

![edit configurations](edit-config-build-watch.png)
