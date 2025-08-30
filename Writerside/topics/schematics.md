# R3DS9 Schematics

The other way to go is to take the angular main street of adopting schematics. Schematics allows to develop generators (among other stuff)
and integrate them into the standard usage of the Angular CLI. When you use `ng generate component` you are using an angular bundled schematics.
Using this approach is possible to envision a process like this one:

- create a definition file (JSON for example) to contain the description of the fields you need and the positioning of these fields.
- operate the generator
- use the artefacts as they are or modify them to customize for specific use.
- in case of re-generation have the schematics create a back-up of changed files
  (or use a different policy, create a diff of some sort to spot differences) in order not to lose the previous work.

We can evaluate the route against a few metrics.

- the forms are separated: no central point that can have regression effects on other code
- the schematics should support the common features. No need for fancy extras: they will be implemented in the generated output
- easy to support different layout-ing options: the two fields query form is very different from the multi section detail form field you
  might require in certain cases and both can be handled the same.

A schematic has been developed to deal with forms. To use in an angular project it is required to

- get the code project from git (the schematics has not been published and cannot be installed with `npm install` or similar commands)
- link the project to the current project by issuing the command `npm link <path-2-schematics-project>`
- use the schematics by issuing the command `ng generate alx-schematics:form <form-component-path-name> ...args.`

The link command from this project is:

`npm link ../../../alexandrya/alx-schematics/alx-schematics`

npm audit

`ng generate component features/sites/components/sites-query-form`
