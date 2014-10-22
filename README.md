# iSENSE Racket
iSENSE Racket is a wrapper around the iSENSE website API written in Racket.  It also includes a library of various utility functions useful when working with intent-related things.

Using iSENSE Racket
-------------------
1. Download or clone this repository.
2. Copy the files `isense-3.rkt` and `quick-net.rkt` into the same directory as the file that is going to call them.
3. Call `(require "isense-3.rkt")` at the top of every file calling iSENSE Racket-related functionality.

`isense-3.rkt` Documentation
----------------------------

Definition | Explanation
--- | ---
`isense-url` | Which version of iSENSE to use - `isenseproject.org` is the production website, while `rsense-dev.cs.uml.edu` is for development.<br>Currently, the only way to change which version of iSENSE you are working with is to modifying the definition of `isense-url` in `isense-3.rkt`.

Function | Explanation
--- | ---
`(isense-project-field name type unit restrictions)` | Creates a field object with a name `name`, a type `type`, a unit of measurement `unit`, and if the field is a text field, `restrictions` determines the allowable values in the field.  It returns the created field object.<br>`unit` is an integer that represents one of the possible field types.  An explanation of which integers represent which field types is available on the iSENSE API documentation page.
`(isense-credentials-ckey ckey name)` | Creates a credentials object based on a contributor key.  `ckey` is the contributor key, and `name` is the contributor name.

`quick-net.rkt` Documentation
-----------------------------