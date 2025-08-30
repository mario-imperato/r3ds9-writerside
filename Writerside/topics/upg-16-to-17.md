# Migrazione da 16 a 17

```
> npm uninstall -g @angular/cli
> npm cache clean –force
> npm install -g @angular/cli@latest
```

A fronte del comando vengono generati una serie di errori del tenore seguente:

```
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: '@angular/cli@17.0.6',
npm WARN EBADENGINE   required: {
npm WARN EBADENGINE     node: '^18.13.0 || >=20.9.0',
npm WARN EBADENGINE     npm: '^6.11.0 || ^7.5.6 || >=8.0.0',
npm WARN EBADENGINE     yarn: '>= 1.13.0'
npm WARN EBADENGINE   },
npm WARN EBADENGINE   current: { node: 'v20.7.0', npm: '10.1.0' }
npm WARN EBADENGINE }
```

facendo supporre che il problema sia il livello di node richiesto `>=20.9.0` (cosa che nella guide non viene menzionato)Inoltre si suggerisce di alzare il livello di npm

```
npm notice 
npm notice New minor version of npm available! 10.1.0 -> 10.2.5
npm notice Changelog: https://github.com/npm/cli/releases/tag/v10.2.5
npm notice Run npm install -g npm@10.2.5 to update!
npm notice 
```

Eseguita l'operazione resta da capire la questione del node.
Di seguito alcuni comandi per il controllo dei livelli e il relativo output.

```
% ng version

Angular CLI: 17.0.6
Node: 20.7.0
Package Manager: npm 10.2.5
OS: darwin arm64

Angular: 
... 

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1700.6 (cli-only)
@angular-devkit/core         17.0.6 (cli-only)
@angular-devkit/schematics   17.0.6 (cli-only)
@schematics/angular          17.0.6 (cli-only)

% node -v
v20.7.0

% npm -v
10.2.5

% tsc -v
Version 5.2.2
```

Tentato un `brew upgrade` che tra le altre cose ha aggiornato (di fatto facendo regredire npm)

```
% node -v
v21.4.0

% npm -v
10.2.4
```

Nella cartella del progetto eseguiti i comandi (tra uno e l'altro eseguire un commit su git per evitare messaggi di disallineamenti):

```
% ng update @angular/core@17 @angular/cli@17
% ng update @angular/material
```

## Angular Schematics

Nota: il comando `npm cache clean –force` sembra non preveda più l'opzione force.

```
% npm uninstall -g @angular-devkit/schematics-cli
% npm cache clean –force
% npm install -g @angular-devkit/schematics-cli
```

Aggiornati poi a mano i seguenti riferimenti ed invocato `npm install`

```
"@angular-devkit/core": "^17.0.6",
"@angular-devkit/schematics": "^17.0.6",
"@angular-devkit/schematics-cli": "^17.0.6",
"@schematics/angular": "^17.0.6",
```

<seealso>
       <category ref="external">
           <a href="https://update.angular.io/?v=16.0-17.0">Guide to update your Angular application v16.0 -> v17.0</a>
       </category>
</seealso>
