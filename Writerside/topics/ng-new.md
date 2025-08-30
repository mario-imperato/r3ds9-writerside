# ng new

Il comando ng new permette la creazione di una app base. 
Nel caso in cui esista gia' un folder con il nome indicato (es. abbiamo clonato un repo git vuoto e vogliamo usare quello come folder di progetto)
&egrave; necessario il folder sia vuoto in quanto il comando ng si lamena se trova un file `README.md` oppure un file `.gitignore`
e riporta un errore di _merge_

> NOTA: il comando ng new &egrave; un buon starting point per capire se esistono eventuali problemi di compatibilit&agrave; 
dei tools (conflitti di dependency sono piuttosto comuni)

La versione della cli utilizzata (linea di comando e output nella stessa sezione)

```
% ng version

Angular CLI: 20.2.1
Node: 24.6.0
Package Manager: npm 11.5.1
OS: darwin arm64
    

Angular: <error>

Package                      Version
------------------------------------
@angular-devkit/architect    0.2002.1 (cli-only)
@angular-devkit/core         20.2.1 (cli-only)
@angular-devkit/schematics   20.2.1 (cli-only)
@schematics/angular          20.2.1 (cli-only)
```

Creaiamo a questo punto il progetto `opem-fe-magazzino`

```
ng new opem-fe-magazzino
```

Se tutto procede senza errori l'output &egrave; il seguente

```
✔ Which stylesheet format would you like to use? Sass (SCSS)     [ https://sass-lang.com/documentation/syntax#scss                ]
✔ Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? No
✔ Do you want to create a 'zoneless' application without zone.js? No
✔ Which AI tools do you want to configure with Angular best practices? https://angular.dev/ai/develop-with-ai None
CREATE opem-fe-magazzino/README.md (1478 bytes)
CREATE opem-fe-magazzino/.editorconfig (314 bytes)
CREATE opem-fe-magazzino/.gitignore (587 bytes)
CREATE opem-fe-magazzino/angular.json (2603 bytes)
CREATE opem-fe-magazzino/package.json (1140 bytes)
CREATE opem-fe-magazzino/tsconfig.json (992 bytes)
CREATE opem-fe-magazzino/tsconfig.app.json (429 bytes)
CREATE opem-fe-magazzino/tsconfig.spec.json (408 bytes)
CREATE opem-fe-magazzino/.vscode/extensions.json (130 bytes)
CREATE opem-fe-magazzino/.vscode/launch.json (470 bytes)
CREATE opem-fe-magazzino/.vscode/tasks.json (938 bytes)
CREATE opem-fe-magazzino/src/main.ts (222 bytes)
CREATE opem-fe-magazzino/src/index.html (301 bytes)
CREATE opem-fe-magazzino/src/styles.scss (80 bytes)
CREATE opem-fe-magazzino/src/app/app.scss (0 bytes)
CREATE opem-fe-magazzino/src/app/app.spec.ts (675 bytes)
CREATE opem-fe-magazzino/src/app/app.ts (300 bytes)
CREATE opem-fe-magazzino/src/app/app.html (20122 bytes)
CREATE opem-fe-magazzino/src/app/app.config.ts (400 bytes)
CREATE opem-fe-magazzino/src/app/app.routes.ts (77 bytes)
CREATE opem-fe-magazzino/public/favicon.ico (15086 bytes)
✔ Packages installed successfully.
    Directory is already under version control. Skipping initialization of git.
```

Da notare un paio di cose:

* e' stato selezionato SCSS per i fogli di stile
* non &egrave; stato attivato un tool di IA (ma questo non per un motivo particolare.... andr&agrave; sperimentato)
* il comando ha trovato una directory git inizializzata (e come detto senza README.md e .gitignore per non avere conflitti)

## Test di esecuzione

```
% cd opem-fe-magazzino
% ng serve
```

L'output che si ottiene:

```

     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/
    


Angular CLI: 20.2.1
Node: 24.6.0
Package Manager: npm 11.5.1
OS: darwin arm64
    

Angular: <error>

Package                      Version
------------------------------------
@angular-devkit/architect    0.2002.1 (cli-only)
@angular-devkit/core         20.2.1 (cli-only)
@angular-devkit/schematics   20.2.1 (cli-only)
@schematics/angular          20.2.1 (cli-only)
(base) marioa.imperato@MACBOOKPRO-64E7 opem % cd opem-fe-magazzin
cd: no such file or directory: opem-fe-magazzin
(base) marioa.imperato@MACBOOKPRO-64E7 opem % cd opem-fe-magazzino
(base) marioa.imperato@MACBOOKPRO-64E7 opem-fe-magazzino % ng serve
Initial chunk files | Names         | Raw size
main.js             | main          | 47.77 kB | 
styles.css          | styles        | 96 bytes | 
polyfills.js        | polyfills     | 95 bytes | 

                    | Initial total | 47.96 kB

Application bundle generation complete. [1.307 seconds]

Watch mode enabled. Watching for file changes...
NOTE: Raw file sizes do not reflect development server per-request transformations.
  ➜  Local:   http://localhost:4200/
  ➜  press h + enter to show help
```

Come si nota questa procedura attiva una componente server che rende disponibile sulla paorta
4200 l'applicazione di sample.

![Ng Hello App](ng-hello-app.png)

## Hello Web Storm

Utilizzando WebStorm si crea un nuovo progetto a partire dai sources generati
ottenendo una cosa di questo genere.

> NOTA: se creiamo il progetto con WebStorm (e lo creiamo dai sources presenti) in ogni caso sembra che
faccia un po' di casino a cominciare dalla modifica del .gitignore e di altri file. Sembra essere necessario _aprirlo_
contando sul fatto che ricrei comunque la cartella .idea

![Hello WebStorm](ng-hello-webstorm.png)

Per eseguire in modalit&agrave; Run o Debug una  applicazione &egrave; necessario far partire un Anuglar Cli Server (in Run o Debug) e successivamente far partire l’applicazione nella detta modalità. 
Da menu’: `Run / Run . . . / Angular Cli Server`.

Una volta partito il terminale è possibile clickare sul link proposto oppure usare 
`Run / Run . . . / Angular Application`

Per il Debug e’ necessario eseguire in sequenza `Run / Debug . . . / Angular CLI Server` e poi 
`Run / Debug . . . / Angular Application`
(La modalità Debug apre una finestra browser dedicata e separata mentre la modalità Run apre tendenzialmente un Tab sul browser)

L'esecuzione dei comandi di run e debug in realt&agrave; non fa altro che eseguire uno script opportunamente parametrizzato.
Per comodit&agrave; di sviluppo ed attivare una modalit&agrave; di hot-reload &egrave; possibile 
inserire uno script all'interno del file package.json. 
Nella sezione scripts inserire `"start-dev": "ng serve --configuration development --verbose"` ottenendo una sezione del tipo seguente:

```json
{
  "name": "opem-fe-magazzino",
  "version": "0.0.0",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "start-dev": "ng serve --configuration development --verbose",
    "build": "ng build",
    "watch": "ng build --watch --configuration development",
    "test": "ng test"
  }
}
```

e selezionarlo all'interno di `Run/Edit Configurations...` dell'interfaccia nel modo seguente.

![WebStorm watch script](ng-serve-watch.png)

Gli script disponibili dalla tendina sono presenti nel file package.json in un frammento come quello seguente:

## ng build

Da terminale &egrave; poi possibile eseguire il comando `ng build` che crea una serie di artefatti
nella cartella `dist` (n.b. la creazione via WebStorm almeno in versione pre 2025.2.1 crea problemi alla versione di build... essenzialmente non builda..)

```
% ng build
Initial chunk files   | Names         |  Raw size | Estimated transfer size
main-6Y32BJHD.js      | main          | 212.46 kB |                58.15 kB
polyfills-5CFQRCPP.js | polyfills     |  34.59 kB |                11.33 kB
styles-5INURTSO.css   | styles        |   0 bytes |                 0 bytes

                      | Initial total | 247.05 kB |                69.48 kB

Application bundle generation complete. [2.399 seconds]

Output location: .../opem-fe-magazzino/dist/opem-fe-magazzino 
```

Viene creata una cartella `dist` con il seguente genere di contenuto:

![dist folder](ng-dist-folder.png)

L'elemento entry point dell'applicazione &egrave; il file `index.html`.  
Questo si differenzia dalle versioni precedenti perch&egrave; non referenzia il file
runtime.js e cambia parzialmente la nomenclatura dei file refernziati
(nella parte che un tempo era occupata da un uuid).

```
<!doctype html>
<html lang="en" data-beasties-container>
<head>
  <meta charset="utf-8">
  <title>OpemFeMagazzino</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
<link rel="stylesheet" href="styles-5INURTSO.css"></head>
<body>
  <app-root></app-root>
  <script src="polyfills-5CFQRCPP.js" type="module"></script>
  <script src="main-6Y32BJHD.js" type="module"></script>
</body>
</html>
```

Prendendo quindi il contenuto della cartella `browser` e spostandolo in una cartella di un server http 
(es: http://my-server/apps/opem-fe-magazzino/) l’applicazione dovrebbe partire. 

## baseHref e deployUrl

In realtà i riferimenti agli script e il valore base href deve essere aggiustato:

* nel caso in esempio o si toglie il base href e tutti I riferimenti diventano relativi, 
* oppure nel base href si pone il riferimento corretto alla sotto cartella di interesse (es. <base href="/apps/opem-fe-magazzino/">)
* alternativamente si puo’ lavorare su entrambi con scopi diversi: 
inserire il base href  e al contempo valorizzare il path degli asset nel caso, ad esempio dovessero essere messi in una cartella separata dall’index.html

Quest'ultimo caso si configura come nel disegno seguente nel quale l'index.html viene prodotto magari dinamicamente
menter lo static content viene servito da una source di tipo CDN.

![Static content](ng-static-content.png)

```
<!doctype html>
<html lang="en" data-beasties-container>
<head>
  <meta charset="utf-8">
  <title>OpemFeMagazzino</title>
  <base href="/url/to/app">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
<link rel="stylesheet" href="/static/styles-5INURTSO.css"></head>
<body>
  <app-root></app-root>
  <script src="/static/polyfills-5CFQRCPP.js" type="module"></script>
  <script src="/static/main-6Y32BJHD.js" type="module"></script>
</body>
</html>
```

L'assegnazione di una base href pu&ograve; essere utile anche durante lo sviluppo dell'applicazione
all'interno dell'IDE. Per farglielo recepire &egrave; necessario eseguire una modifica al file
`angular.json`. L'immagine che segue riporta la posizione nel file dove inserire la configurazione
`"baseHref": "/url/to/app/"` (gli slash sono rilevanti....) evidenziando il path della propriet&agrave; `development` sulla quale intervenire.

![NG Base Href](ng-base-href.png)

Una volta effettuata questa configurazione si verifica che al run dell'applicazione 
(che noi abbiamo precedentemente configurato con lo script start-dev) la IDE monta l'applicazione sotto al 
path richiesto.

```
Initial chunk files | Names         | Raw size
main.js             | main          | 47.77 kB | 
styles.css          | styles        | 96 bytes | 
polyfills.js        | polyfills     | 95 bytes | 

                    | Initial total | 47.96 kB

Application bundle generation complete. [0.967 seconds]

Watch mode enabled. Watching for file changes...
NOTE: Raw file sizes do not reflect development server per-request transformations.
  ➜  Local:   http://localhost:4200/url/to/app
  ➜  press h + enter to show help
```

Facendo attenzione si vede che la sezione `development` vede la valorizzazione della sola propriet&agrave; addizionale
`baseHref` mentre la sezione `production` configura anche la propriet&agrave;
`deployUrl`. Questa ulteriore configurazione permette se serve di configurare ulteriormente un path diverso per 
i contenuti statici rispetto al path che viene visto dalla applicazione (curiosamente questo parametro - piuttosto usato - era stato deprecato qualche versione fa ma
poi lasciato in seguito a vigorose proteste degli sviluppatori)

```
<!doctype html>
<html lang="en" data-beasties-container>
<head>
  <meta charset="utf-8">
  <title>OpemFeMagazzino</title>
  <base href="/url/to/app/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
<link rel="stylesheet" href="/path/to/static/styles-5INURTSO.css"></head>
<body>
  <app-root></app-root>
  <script src="/path/to/static/polyfills-5CFQRCPP.js" type="module"></script>
  <script src="/path/to/static/main-6Y32BJHD.js" type="module"></script></body>
</html>
```
