# gen: sotto comando svc

> Nota: alcuni aspetti di questo comando verranno rivisti perche&egrave; poco _seamless_

```
Usage:
  tpm-gong-schematics-cli gen svc [flags]

Flags:
  -e, --deps string   dependencies of the project in the form <ambit>:<path>[#<context-name>]
  -h, --help          help for svc
  -n, --name string   base name of the artifacts
  -k, --with-bak      the current artifacts if present will be backed-up and a diff file produced
  -d, --with-ds       skeleton code for data source is created
  -f, --with-flat     if set to true the stuff is created in a subfolder named after the name of the object, if not, it is created into the parent
  -w, --with-new      if the current artifacts is present the new one will be written to a .new file and a diff file produced
  -s, --with-store    skeleton code for store is created
```

Questo comando crea alcuni artefatti per la invocazione di servizi nel bak-end rest.

Nella sua modalit&agrave; _base_ genera uno skeleton per l'invocazione di endpoint.

| parametro  | note                                                                                                                                                                                                                                                |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| name       | path name e nome dell'endpoint sempre relativo alla root del progetto Angular                                                                                                                                                                       |
| deps       | nella generazione viene referenziata l'interfaccia del tipo di dato che viene ritornato: in questo caso si inserisce il riferimento di una interfaccia prodotta via comando types. Il parametro &egrave; nella forma <path>#<nome dell'interfaccia> |
| with-ds    | produce un file che implementa l'interfaccia DataSource prevista da Angular.                                                                                                                                                                        |
| with-store | produce un file che pu&ograve; essere usato come Store                                                                                                                                                                                              |

```sh
gong-schematics-cli gen svc  \
    --name /src/app/api/core/kv2/services/key-value-package \
    --deps types:/src/app/store/r3ds9-apicore/keyvaluepackage/key-value-package#KeyValuePackage \
    --with-flat
```

con questo comando vengono generati i seguenti file (la nomenclatura dei file ovviamente dipende dal parametro `name`):

* README.md: contenente un semplice markdown che riporta il comando usato per generare gli artefatti; di utilit&agrave; in caso di necessit&agrave; di nuova esecuzione ed eventualmente per inserire note
* endpoint.config.ts: i riferimenti agli endpoint con il loro mapping
* key-value-package.endpoint.ts: il codice vero e proprio che deve essere modificato

Nel caso in cui vengano specificati gli ulteriori due parmetri si ottengono alcuni file addizionali.

* `with-ds`: viene generato il file `key-value-package.ds.ts`
* `with-store`: `key-value-package.store.ts` e `key-value-package.store-state.ts` due asset funzionali per il modello di store adottato
