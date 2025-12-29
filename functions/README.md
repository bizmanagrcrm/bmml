# BMML Functions

### `(pageUrl, [paramsObj])`
This function is used to redirect the user to a specific page, using the url.
(Note, this is internal routing, not a full page reload)
`paramsObj` is an optional argument of an object to be passed as parameters to the url

Example:
```<button ng-click="goToPageByUrl('/home')">Go to home</button>```

Note, you can use {{}} to bind the url to a variable.


### `goToExternalUrl(url, [newTab])`

The first argument is the url to redirect to. The second argument is a boolean value that indicates if the url should be opened in a new tab. (default: false)

This function is used to redirect the user to an external url (for example, a website).

Example:
```<button ng-click="goToExternalUrl('https://www.twitter.com/{{profile}}')">Go to twitter profile</button>```

Note, you can use {{}} to bind the url to a variable.


### `getFormattedDate(format, [date])`

The first argument is the format of the date. For format options, see [here](https://docs.angularjs.org/api/ng/filter/date).

 The second argument is the date to format. (default: current date)


### `executeActionByName(tableName, actionName, data, scope, options)`
The first argument is the internal name of the table that the action is attached to.

The second argument is the internal name of the action to execute.

The third argument is the data to send to the action. For system actions, this is usually the record object. For custom actions, this is any data you want to send to the action.
If the action is a custom action, the data will be available in the action code in the `record` variable.
There is also a `scope` variable available in the action code. This variable contains the scope of the view that the action was triggered from.
The fourth argument is the scope of the view that triggered the action. If not provided, the function falls back to **this** which will normally be the scope where the call originated (i.e., the caller's scope). If the function is invoked explicitly via $root(i.e., $root.executeActionByName(...)), **this** will be **$rootScope**, The resulting scope is available as a variable `scope`in the action code. This argument usually does **not** need to be past.
The fifth argument is an options object. This object can contain the following properties:
- `promiseMode` - if set to true, the function will return a promise that resolves when the action is completed. (default: false)
- `failSilently` - if set to true, the function will not show any error messages if the action fails. (default: true)

### `isArray(value)`

 This is the angular isArray function. see [here](https://docs.angularjs.org/api/ng/function/angular.isArray)


### `dismissModal(reason)`

This function is used to close a modal. The first argument is the data to send back to the parent controller. (default: null)
Note, this function is only available in modals.
