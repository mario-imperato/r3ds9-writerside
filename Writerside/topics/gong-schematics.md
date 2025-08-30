# gong-schematics-cli

`gong-schematics-cli` &egrave; un tool a linea di comando per la generazione di alcuni artefatti di progetto.
Vuole mimare le funzionalit&agrave; schematics ma scritte in golang e dal punto di vista dello _scrivente_ pi&ugrave; facilmente gestibili.

Questa CLI utilizza la libreria Cobra e mette a disposizione una serie di comandi e sottocomandi.

Usage:

```shell
gong-schematics-cli [command] [sub-command] [OPTIONS]
```

## Commands
Se non viene specificato nessun command l'output e' del tipo seguente con alcune informazioni di help.
Il comando effettivamente disponibile &egrave; `gen`

```plain text
|__   __|  __ \|  \/  |       / ____|     | \ | |            / ____|    | |                        | | (_)
    | |  | |__) | \  / |______| |  __  ___ |  \| | __ _ _____| (___   ___| |__   ___ _ __ ___   __ _| |_ _  ___ ___
    | |  |  ___/| |\/| |______| | |_ |/ _ \| . ` |/ _` |______\___ \ / __| '_ \ / _ \ '_ ` _ \ / _` | __| |/ __/ __|
    | |  | |    | |  | |      | |__| | (_) | |\  | (_| |      ____) | (__| | | |  __/ | | | | | (_| | |_| | (__\__ \
    |_|  |_|    |_|  |_|       \_____|\___/|_| \_|\__, |     |_____/ \___|_| |_|\___|_| |_| |_|\__,_|\__|_|\___|___/
                                                   __/ |
                                                  |___/


Version: v0.0.1
Sha: SHA
The command line supports the generation of some artifacts targeted at angular projects.

Usage:
  gong-schematics-cli [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  gen         command for generating artifacts in an angular project
  help        Help about any command

Flags:
  -h, --help      help for tpm-gong-schematics-cli
      --verbose   verbose output

Use "gong-schematics-cli [command] --help" for more information about a command.
```

Al momento l'unico comando disponibile &egrave; il gen che prevede alcuni sottocomandi.

