# BMML Functions

### `goToPageByUrl(pageUrl)`
This function is used to redirect the user to a specific page, using the url.
(Note, this is internal routing, not a full page reload)

Example:
```<button ng-click="goToPageByUrl('/home')">Go to home</button>```

Note, you can use {{}} to bind the url to a variable.


### `goToExternalUrl(url, newTab)`

The first argument is the url to redirect to. The second argument is a boolean value that indicates if the url should be opened in a new tab. (default: false)

This function is used to redirect the user to an external url (for example, a website).

Example:
```<button ng-click="goToExternalUrl('https://www.twitter.com/{{profile}}')">Go to twitter profile</button>```

Note, you can use {{}} to bind the url to a variable.