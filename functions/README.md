# BMML Functions

### `goToPageByUrl(pageUrl)`
This function is used to redirect the user to a specific page, using the url.
(Note, this is internal routing, not a full page reload)

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


### `executeActionByName(tableName, actionName, data)`
The first argument is the internal name of the table that the action is attached to.
The second argument is the internal name of the action to execute.
The third argument is the data to send to the action. For system actions, this is usually the record object. For custom actions, this is any data you want to send to the action.
If the action is a custom action, the data will be available in the action code in the `record` variable.
There is also a `scope` variable available in the action code. This variable contains the scope of the view that the action was triggered from.

### `isArray(value)`

 This is the angular isArray function. see [here](https://docs.angularjs.org/api/ng/function/angular.isArray)


### `dismissModal(reason)`

This function is used to close a modal. The first argument is the data to send back to the parent controller. (default: null)
Note, this function is only available in modals.
