# iSENSE Racket
iSENSE Racket is a wrapper around the iSENSE website API written in Racket.  It also includes a library of various utility functions useful when working with intent-related things.

Below is a brief explanation of the content of these two files, and what they do.  For a more detailed explanation, look at the inline documentation.  Also, the code is fairly self-explanatory.  If you have any questions, feel free to ask.

There's probably still a couple bugs, most of which are probably related to handling errors resulting from not having the correct permissions to upload data to a project.  In the mean time, don't do that.  Alternatively, you could do that and try to recover from the errors.  Both work with varying degrees of success.

Using iSENSE Racket
-------------------
1. Download or clone this repository.
2. Copy the files `isense-3.rkt` and `quick-net.rkt` into the same directory as the file that is going to call them.
3. Call `(require "isense-3.rkt")` at the top of every file calling iSENSE Racket-related functionality.

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
* `(isense-create-project cred name fields)`: Creates a project on iSENSE.
* `(isense-add-field project cred type name units (restrictions ""))`: Adds a field to a project.
* `(isense-add-dataset project cred data name)`: Adds a dataset to a project.
* `(isense-append-dataset dset cred data)`: Appends data to a dataset.  Currently does not work.

There are project, dataset, field, and credential objects.  For an explanation of how to use each one, look up the accompanying `make-x` function in the source, where `x` is the name of the object.  None of these functions should be publicly accessible, but the method of accessing their data is important and contained within each.

`quick-net.rkt` Documentation
-----------------------------
* `(read-str-all port)`: Reads all of the data from a Racket port.
* `(get-webpage url)`: Gets a webpage.  If it fails to load the page, it will retry until it eventually works.  404s, 422s, 505s, etc... don't count as the page failing to load, so bad requests *shouldn't* repeat indefinitely.
* `(read-str-all port)`: Encodes URLs so they don't blow up.
* `(index lst)`: Given a list, create a list of lists where each entry in the original list is numbered starting from one.
* `(list-range lst start end)`: Takes a zero-index start and end position, and returns a list containing the data between those two points.
* `(list-partition lst parts)`: Takes a list and divides it into identicaly sized parts.
* `(timed-map time)`: Returns a version of map that runs for a certain amount of time before prematurely terminating, returning only the results obtained up to that point.
* `(timed-filter time)`: Returns a version of filter taht runs for a certain amount of time before prematurely terminating, returning only the results obtaind up to that points.
* `(apply-batch op proc threads lst-args)`: Distributes a call to map, filter, timed-map, or timed-filter across an arbitrary number of threads and returns the result.
* `(json-burrow jsexpr . lst)`: Kind of like CSS selectors in jQuery.  Retrieves data from a JSON structure, or returns false if the path specified is not valid.  Paths consist of symbols (for objects), integers (for arrays), and #t (for picking the first thing in a JSON object).

The functions in `quick-net.rkt` were created in response to the needs of an application I wrote that did lots of web-based batch processing.  `isense-3.rkt` uses some of this functionality, but certain functions like `timed-map` and `apply-filter` aren't and should be entirely useless to most people using this library.