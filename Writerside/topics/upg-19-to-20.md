# Migrazione da 19 a 20

```
> npm uninstall -g @angular/cli
> npm cache clean -force
> npm install -g @angular/cli@20
```

Nella disinstallazione della cli viene suggerito di upgradar npm.

```
npm notice
npm notice New minor version of npm available! 11.2.0 -> 11.5.2
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.5.2
npm notice To update run: npm install -g npm@11.5.2
npm notice
```

Di seguito alcuni comandi per il controllo dei livelli e il relativo output.

```
% ng version

Angular CLI: 20.1.6
Node: 24.6.0
Package Manager: npm 11.5.1
OS: darwin arm64

Angular: 
... 

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.2001.6 (cli-only)
@angular-devkit/core         20.1.6 (cli-only)
@angular-devkit/schematics   20.1.6 (cli-only)
@schematics/angular          20.1.6 (cli-only)

% node -v
v24.6.0

% npm -v
11.5.1

% tsc -v
Version 5.8.2
```

## Cartella di progetto

Nella cartella del progetto eseguiti i comandi (tra uno e l'altro eseguire un commit su git per evitare messaggi di disallineamenti).
La procedura chiede se si vuole migrare al nuovo [build-system](https://angular.dev/tools/cli/build-system-migration). Risposto OK.

```
% ng update @angular/core@20 @angular/cli@20
```

Output

```
The installed Angular CLI version is outdated.
Installing a temporary Angular CLI versioned 20.1.6 to perform the update.
(node:17948) [DEP0190] DeprecationWarning: Passing args to a child process with shell option true can lead to security vulnerabilities, as the arguments are not escaped, only concatenated.
(Use `node --trace-deprecation ...` to show where the warning was created)
Using package manager: npm
Collecting installed dependencies...
Found 29 dependencies.
Fetching dependency metadata from registry...
    Updating package.json with dependency @angular-devkit/build-angular @ "20.1.6" (was "19.2.3")...
    Updating package.json with dependency @angular/cli @ "20.1.6" (was "19.2.3")...
    Updating package.json with dependency @angular/compiler-cli @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency typescript @ "5.8.3" (was "5.5.4")...
    Updating package.json with dependency @angular/animations @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency @angular/common @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency @angular/compiler @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency @angular/core @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency @angular/forms @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency @angular/platform-browser @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency @angular/platform-browser-dynamic @ "20.1.7" (was "19.2.2")...
    Updating package.json with dependency @angular/router @ "20.1.7" (was "19.2.2")...
UPDATE package.json (1354 bytes)
✔ Cleaning node modules directory
✔ Installing packages

(node:17953) [DEP0190] DeprecationWarning: Passing args to a child process with shell option true can lead to security vulnerabilities, as the arguments are not escaped, only concatenated.                                                                                                                                              
(Use `node --trace-deprecation ...` to show where the warning was created)                                                                                           
** Executing migrations of package '@angular/cli' **
                                                                                                                                                                     
❯ Update workspace generation defaults to maintain previous style guide behavior.
UPDATE angular.json (7159 bytes)
  Migration completed (1 file modified).

❯ Migrate imports of 'provideServerRendering' from '@angular/platform-server' to '@angular/ssr'.
  Migration completed (No changes made).

❯ Migrate 'provideServerRendering' to use 'withRoutes', and remove 'provideServerRouting' and 'provideServerRoutesConfig' from '@angular/ssr'.
  Migration completed (No changes made).

❯ Update 'moduleResolution' to 'bundler' in TypeScript configurations.
  You can read more about this, here: https://www.typescriptlang.org/tsconfig/#moduleResolution
UPDATE tsconfig.json (901 bytes)
  Migration completed (1 file modified).

** Optional migrations of package '@angular/cli' **
                                                                                                                                                                     
This package has 1 optional migration that can be executed.
Optional migrations may be skipped and executed after the update process, if preferred.

 Select the migrations that you'd like to run [use-application-builder] Migrate application projects to the new build system. 
(https://angular.dev/tools/cli/build-system-migration)

❯ Migrate application projects to the new build system.
  Application projects that are using the '@angular-devkit/build-angular' package's 'browser' and/or 'browser-esbuild' builders will be migrated to use the new 'application' builder.
  You can read more about this, including known issues and limitations, here: https://angular.dev/tools/cli/build-system-migration
UPDATE package.json (1338 bytes)
UPDATE angular.json (7099 bytes)
✔ Packages installed successfully.
  Migration completed (2 files modified).

** Executing migrations of package '@angular/core' **
                                                                                                                                                                     
❯ Moves imports of `DOCUMENT` from `@angular/common` to `@angular/core`.
  Migration completed (No changes made).

❯ Replaces usages of the deprecated InjectFlags enum.
  Migration completed (No changes made).

❯ Replaces usages of the deprecated TestBed.get method with TestBed.inject.
  Migration completed (No changes made).

** Optional migrations of package '@angular/core' **
                                                                                                                                                                     
This package has 1 optional migration that can be executed.
Optional migrations may be skipped and executed after the update process, if preferred.

 Select the migrations that you'd like to run 
```

```
% ng update @angular/material@20
```

## Angular Schematics

Nota: il comando `npm cache clean –force` sembra non preveda più l'opzione force.

```
% npm uninstall -g @angular-devkit/schematics-cli
% npm cache clean –force
% npm install -g @angular-devkit/schematics-cli@20
```

<seealso>
       <category ref="external">
           <a href="https://angular.dev/update-guide?v=19.0-20.0&l=2">Guide to update your Angular application v19.0 -> v20.0</a>
       </category>
</seealso>
