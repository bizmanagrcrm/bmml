# BMML Elements


### `<bmml-report>`
This element is used to embed a report in the page. The report is identified by its id.
example:
```<bmml-report id="1"></bmml-report>```



## BMML Functions

### `goToPageByUrl(pageUrl)`
This function is used to redirect the user to a specific page, using the url.
(Note, this is internal routing, not a full page reload)

Example:
```<button ng-click="goToPageByUrl('/home')">Go to home</button>```

Note, you can use {{}} to bind the url to a variable.