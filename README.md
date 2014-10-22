# iSENSE Racket
iSENSE Racket is a wrapper around the iSENSE website API written in Racket.  It also includes a library of various utility functions useful when working with intent-related things.

Using iSENSE Racket
-------------------
1. Download or clone this repository.
2. Copy the files `isense-3.rkt` and `quick-net.rkt` into the same directory as the file that is going to call them.
3. Call `(require "isense-3.rkt")` at the top of every file calling iSENSE Racket-related functionality.

Below is a brief explanation of the content of these two files, and what they do.  For a more detailed explanation, look at the inline documentation.

`isense-3.rkt` Documentation
----------------------------

* `isense-url`: Which version of iSENSE to use - `isenseproject.org` is the production website, while `rsense-dev.cs.uml.edu` is for development.<br>Currently, the only way to change which version of iSENSE you are working with is to modifying the definition of `isense-url` in `isense-3.rkt`.
* `(isense-project-field name type unit restrictions)`: Creates a field object.
* `(isense-credentials-ckey ckey name)`: Creates a credentials object based on a contributor key.  `ckey` is the contributor key, and `name` is the contributor name.
* `(isense-credentials-pass email pass)`: Creates a credentials object based on an email and password.
* `(isense-search str (sort "updated_at") (order "DESC") (count -1))`: Search projects on iSENSE for a string with the given search parameters.
* `(isense-get-project-by-id id)`: Find a project and return a project object based on the given project id.
* `(isense-get-dataset-by-id id)`: Find a dataset and return a dataset object based on the given dataset id.
* `(isense-get-field-by-id id)`: Find a field and return a field object based on the given field id.
* `(isense-create-project cred name fields)`: Creates a project on iSENSE
* `(isense-add-field project cred type name units (restrictions ""))`: Adds a field to a project

`quick-net.rkt` Documentation
-----------------------------