# Configurazione Multi Tenancy

Dopo aver descritto la configurazione di una Angular App torniamo alla questione multi-tenancy.
Nella ipotesi descritta si presentano le seguenti esigenza:

* a fronte di un url strutturato in termini di una quaterna (_appType_, _domain_, _site_ e _appId_) viene selezionata l'app corretta e ritornato un `index.html`
* i riferimenti interni al contenuto js sono posizionati su URL differenti erogati in maniera statica
* &egrave; necessario supportare le modalit&agrave; di _produzione_ e _debug_.

## Produzione

L'obiettivo &egrave; produrre qualcosa di questo genere: a fronte di una chiamata:

```
https://localhost:8080/ui-admin/card/edenred/app-home/....
```

generare un `index.html` del tipo seguente.

```
<!doctype html>
<html lang="en" data-beasties-container>
<head>
  <meta charset="utf-8">
  <title>OpemFeMagazzino</title>
  <base href="/ui-admin/card/edenred/app-home">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
<link rel="stylesheet" href="/static/webapps/app-home/styles-5INURTSO.css"></head>
<body>
  <app-root></app-root>
  <script src="/static/webapps/app-home/polyfills-5CFQRCPP.js" type="module"></script>
  <script src="/static/webapps/app-home/main-6Y32BJHD.js" type="module"></script>
</body>
</html>
```

Durante la fase di build quindi &egrave; necessario predisporre un html passibile di personalizzazione
da parte di una componente server non essendo noti a priori le valorizzazioni della quaterna.
Per far questo &egrave; semplicemente possibile configurare baseHref e deployUrl con una struttura di place-holders
che vengono rimpiazzati server-side.

Per far questo possiamo valorizzare le due variabili presenti in `angular.json` nella sezione `production`
nella maniera seguente:

```
"baseHref": "/__appType__/__domainId__/__siteId__/__language__/__appId__/", 
"deployUrl": "__static_path_to_webapps__/opem-ge-magazzino/"
```

Osserviamo quanto segue:

* `baseHref` &egrave; valorizzato con un formato a place-holder con indicazione della quaterna.
* `deployUrl`: vede la presenza di un ulteriore place-holder per permettere la configurazione server side 
del path desiderato per l'esposizione degli asset statici.

Con questa config ed eseguendo il comando `ng build -c production` si ottiene un `index.html` del tipo seguente

```html
<!doctype html>
<html lang="en" data-beasties-container>
<head>
  <meta charset="utf-8">
  <title>OpemFeMagazzino</title>
  <base href="/__appType__/__domainId__/__siteId__/__language__/__appId__/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
<link rel="stylesheet" href="__static_path_to_webapps__/opem-ge-magazzino/styles-5INURTSO.css"></head>
<body>
  <app-root></app-root>
  <script src="__static_path_to_webapps__/opem-ge-magazzino/polyfills-5CFQRCPP.js" type="module"></script>
  <script src="__static_path_to_webapps__/opem-ge-magazzino/main-6Y32BJHD.js" type="module"></script>
</body>
</html>
```

Dal _build_ ottenuto in questo modo sar&agrave; poi necessario copiare gli asset relativi in modo che siano 
accessibili alla/alle componente/i server in modo da poter essere utilizzate. La location fisica pu&ograve; differire
tra index.html e asset statici oppure si pu&ograve; ipotizzare una copia doppia integrale.

## Development
Questa modalit&agrave; si presenta pi&ugrave; complessa per due ordini di motivi:

* non esiste nessuna componente server in grado di eseguire la risoluzione e quindi questa risoluzione deve risultare
pre-configurata.
* pre-configurare significa che in questa modalit&agrave; non &egrave; possibile cambiare uno dei 4 parametri
chiave di risoluzione direttamente nel browser proprio perch&egrave; la quaterna risulta cablata.
* l'applicazione viene resa disponibile tramite porta 4200 mentre gli eventuali servizi rest della business logic rimangono 
deployati su un server diverso (es. localhost:8080): perch&egrave; l'applicazione funzioni &egrave; necessario predisporre questo doppio instradamento;
questa cosa &egrave; possibile utilizzando la funzionalit&agrave; di proxy presente in Angular
(n.b. una situazione di produzione &egrave; diversa in quanto entrambi gli url sono serviti - o proxati - dallo stesso host)

### Modifica angular.json
La prima modifica da attuare &egrave; quella di inserire la valorizzazione baseHref. 
In questo caso, per quanto detto circa l'assenza di un elemento server side di risoluzione, dobbiamo immettere
un url fatto e finito e senza place holder:

```
"baseHref": "/admin_ui/card/edenred/it/app-magazzino/", 
```

Cos&igrave; facendo se eseguiamo il run dell'Application Server otteniamo come output:

```
Initial chunk files | Names         | Raw size
main.js             | main          | 47.77 kB | 
styles.css          | styles        | 96 bytes | 
polyfills.js        | polyfills     | 95 bytes | 

                    | Initial total | 47.96 kB

Application bundle generation complete. [1.076 seconds]

Watch mode enabled. Watching for file changes...
NOTE: Raw file sizes do not reflect development server per-request transformations.
  ➜  Local:   http://localhost:4200/admin_ui/card/edenred/it/app-magazzino
```

Ovvero la IDE ci propone correttamente l'url di mount dell'applicazione 
(come segnalato, per cambiarlo &egrave; necessario modificare manualmente angular.json)

Questa modifica tuttavia non sembra bastare per attivare la modalit&agrave; debug per la quale &egrave; necessario far partire
il server e l'applicazione separatamente in modalit&agrave; debug. &egrave; necessario entrare in `Run / Edit Configurations...`
ed editare la configurazione della application sostituendo al `http://localhost:4200` (vedi figura successiva)

![NG Application Run Config](ng-application-run-config.png)

con `http://localhost:4200/admin_ui/card/edenred/it/app-magazzino` come nell'esempio seguente:

![NG Application Modified Run Config](ng-application-run-mod-config.png)

Come si pu&ograve; notare abbiamo 'cablato' l'url gi&agrave; due volte.

### Proxy configuration

In modalit&agrave; di sviluppo si hanno due server:

* il primo instanziato dalla IDE e che risponde sulla porta 4200
* il secondo invece il server con la business logic che in modalit&agrave; sviluppo pu&ograve; essere
`localhost:8080`.

Esiste un meccanismo di proxy locale client che permette di _routare_ le richieste 
verso il server con la business logic e inoltrare le richieste della UI sulla porta 4200.
Questa funzionalit&agrave; in config si attiva prevedendo il file `proxy.conf.json` 
nella cartella `src` e refernziandolo in `angular.json` come nella figura che segue.

![NG Proxy Config](ng-proxy-config.png)

Un esempio di configurazione &egrave; la seguente che instrada tutti gli url che iniziano con `/api`
verso `localhost:8080`.

```
{
  "/api": {
    "target": "http://localhost:8080",
    "secure": false,
    "logLevel": "debug",
    "changeOrigin": true
  }
}
```
