# Migrazione da 18 a 19

> *NOTA* L'upgrade a doppia versione non e' supportato onde per cui e' necessario operare per gradi passando dalla 17.0 alla 18.0

```
> npm uninstall -g @angular/cli
> npm cache clean -force
> npm install -g @angular/cli@19
```

Di seguito alcuni comandi per il controllo dei livelli e il relativo output.

```
% ng version

Angular CLI: 19.2.3
Node: 23.10.0 (Unsupported)
Package Manager: npm 11.2.0
OS: darwin arm64

Angular: 
... 

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1902.3 (cli-only)
@angular-devkit/core         19.2.3 (cli-only)
@angular-devkit/schematics   19.2.3 (cli-only)
@schematics/angular          19.2.3 (cli-only)
    
Warning: The current version of Node (23.10.0) is not supported by Angular.

% node -v
v23.10.0

% npm -v
11.2.0

% tsc -v
Version 5.8.2
```

## Cartella di progetto

Nella cartella del progetto eseguiti i comandi (tra uno e l'altro eseguire un commit su git per evitare messaggi di disallineamenti).
La procedura chiede se si vuole migrare al nuovo [build-system](https://angular.dev/tools/cli/build-system-migration). Risposto OK.

```
% ng update @angular/core@19 @angular/cli@19
% ng update @angular/material@19
```

Vengono poi proposte un paio di opzioni di selezione. Al momento selezionati i default.

* The output location of the browser build has been updated from "dist/r3ds9-admin-app-home" to "dist/r3ds9-admin-app-home/browser". You might need to adjust your deployment pipeline or, as an alternative, set outputPath.browser to "" in order to maintain the previous functionality.
* Select the migrations that you'd like to run (Press <space> to select, <a> to toggle all, <i> to invert selection, and <enter> to proceed): [provide-initializer] Replaces `APP_INITIALIZER`, `ENVIRONMENT_INITIALIZER` & `PLATFORM_INITIALIZER` respectively with `provideAppInitializer`, `provideEnvironmentInitializer` & `providePlatformInitializer`.

## Angular Schematics

Nota: il comando `npm cache clean –force` sembra non preveda più l'opzione force.

```
% npm uninstall -g @angular-devkit/schematics-cli
% npm cache clean –force
% npm install -g @angular-devkit/schematics-cli@19
```

<seealso>
       <category ref="external">
           <a href="https://angular.dev/update-guide?v=18.0-19.0&l=1">Guide to update your Angular application v18.0 -> v19.0</a>
       </category>
</seealso>
