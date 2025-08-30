# Migrazione da 15 a 16

```
> npm uninstall -g @angular/cli
> npm cache clean –force
> npm install -g @angular/cli@latest
> ng update @angular/cli
```

```
> npm install -g typescript
> npm install typescript@4.9.4 --save-dev
> npm install @types/node@latest @types/jasmine@latest --save-dev
> npm install @angular-devkit/build-angular@latest @angular/compiler-cli@latest @angular/language-service@latest --save-dev
```

```
> npm install rxjs@latest rxjs-compat@latest –save
> npm install @angular/animations@latest @angular/common@latest @angular/compiler@latest @angular/core@latest @angular/forms@latest @angular/http@latest @angular/platform-browser@latest @angular/platform-browser-dynamic@latest @angular/platform-server@latest @angular/router@latest –save
> npm install core-js@latest zone.js@latest –save
> ng update @angular/core 
```

> **NOTA** Per il typescript all’interno del singolo Progetto puo’ essere necessario non avere la latest. In questo caso usata la 4.9.4 che sembra non dare errori di dipendenza.
> **NOTA** (all’interno del singolo progetto)

## Angular Schematics

```
> npm uninstall -g @angular-devkit/schematics-cli
> npm cache clean –force
> npm install -g @angular-devkit/schematics-cli
```

Poi da linea di commando ho tentato vari update ma senza molta fortuna. Quello che poi ho provato è stato andare su package.json nella sezione dependencies e dire ‘Aggiorna alla versione… Dove la IDE mi dice la versione. Poi ho fatto un npm install che ha i-aggiornato un po’ tutto.
Diciamo che si tratta di un TODO per capire come si deve fare…

<seealso>
       <category ref="external">
           <a href="https://www.codeproject.com/Articles/5360980/Angular-Migration-to-16">Angular Migration to 16</a>
           <a href="https://stackoverflow.com/questions/75037687/angular-14-cli-is-not-compatible-with-node-version-18-12-1">Angular 14 CLI is not compatible with node version 18.12.1</a>
           <a href="https://www.freecodecamp.org/news/how-to-update-npm-dependencies/">How to Update NPM Dependencies</a>
       </category>
</seealso>


