# Migrazione da 17 a 18

> *NOTA* L'upgrade a doppia versione non e' supportato onde per cui e' necessario operare per gradi passando dalla 17.0 alla 18.0

```
> npm uninstall -g @angular/cli
```

In questa fase in corrispondenza di `npm uninstall -g @angular/cli`

```
npm notice
npm notice New major version of npm available! 10.9.0 -> 11.2.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.2.0
npm notice To update run: npm install -g npm@11.2.0
npm notice
```

eseguiamo il suggerito aggiornamento npm con `npm install -g npm@11.2.0`

```
> npm cache clean -force
> npm install -g @angular/cli@18
```

Di seguito alcuni comandi per il controllo dei livelli e il relativo output.

```
% ng version

Angular CLI: 18.2.15
Node: 23.10.0 (Unsupported)
Package Manager: npm 11.2.0
OS: darwin arm64

Angular: 

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1802.15 (cli-only)
@angular-devkit/core         18.2.15 (cli-only)
@angular-devkit/schematics   18.2.15 (cli-only)
@schematics/angular          18.2.15 (cli-only)
    
Warning: The current version of Node (23.10.0) is not supported by Angular.

% node -v
v23.10.0

% npm -v
11.2.0

% tsc -v
Version 5.2.2
```

Eseguito upgrade di typescript: `npm install -g typescript`. Eseguendo il comand `tsc -version` si ottiene

```
Version 5.8.2
```

## Cartella di progetto

Nella cartella del progetto eseguiti i comandi (tra uno e l'altro eseguire un commit su git per evitare messaggi di disallineamenti).
La procedura chiede se si vuole migrare al nuovo [build-system](https://angular.dev/tools/cli/build-system-migration). Risposto OK.

```
% ng update @angular/core@18 @angular/cli@18
% ng update @angular/material@18
```

L'upgrade di Angular Material ha prodotto una modifica su alcuni file scss con alcune righe cambiate nel modo seguente:

```
From ---> $color-config: mat.get-color-config($theme);
To   ---> $color-config: mat.m2-get-color-config($theme);
```

## Angular Schematics

Nota: il comando `npm cache clean –force` sembra non preveda più l'opzione force.

```
% npm uninstall -g @angular-devkit/schematics-cli
% npm cache clean –force
% npm install -g @angular-devkit/schematics-cli@18
```

<seealso>
       <category ref="external">
           <a href="https://angular.dev/update-guide?v=17.0-18.0&l=1">Guide to update your Angular application v17.0 -> v18.0</a>
       </category>
</seealso>
