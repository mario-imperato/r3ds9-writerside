# Creare una nuova applicazione

In questa sezione riportiamo le informazioni utili per la creazione
di una nuova app per la piattaforma.

I passi che vengono illustrati sono passi manuali (senza supporto gong-schematics) tramite comandi `ng`
e `npm`. Principalmente consideriamo l'uso di WebStorm come ambiente di sviluppo sebbene si possano usare
anche Visual Studio o Eclipse

Le funzionalità della piattaforma sono divise in due gruppi principali: 

* funzionalità utente: questa modalit&agrave; &egrave; per utenti che hanno una forma di self-registration e utilizzano alcune funzionalit&agrave;; pu&ograve; mancare in alcuni ambiti.
* funzionalità di amministrazione: in generale sempre presente.

L’url per l’accesso alla applicazione &egrave; del seguente tipo:

```
http://localhost:8080/<app-type>/<domain>/<namespace>/<language>/<app-id>/...
```

* app-type: distingue l’ambito dell’applicazione (valori: ui oppure ui-console).
* domain: i namespace sono organizzati all’interno di un namespace superior chiamato dominio che ha scopi di aggregazione di namespace appartenenti ad uno stesso Gruppo amministrativo.
* namespace:  identificativo del namespace utilizzato come element logico di configurazione e profilazione
* language: linguaggio richiesto (al momento non implementato ma previsto)
* app-id: identificativo dell’App.

Questo url viene risolto server side per restituire l'index.html corretto per la cinquina di valori indicati: si tratta di un url dinamico 
per permettere lato server di associare app diverse allo stesso url o per bloccare, eventualmente, l'accesso a certi utenti.
L'index.html che viene ritornato al suo interno contiene poi i riferimenti all'effettivo _corpo_ della applicazione.
Per permettere una corretta gestione del tutto dal punto di vita dello sviluppo saranno necessarie alcune config da effettuare.
Andiamo comunque in ordine.



