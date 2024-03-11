# BMML Filters

On top of Angular.js built-in filters, we have added some custom filters that you can use in your custom code.

To read about Angular.js built-in filters, please visit [Angular.js documentation](https://code.angularjs.org/1.8.0/docs/api/ng/filter/filter)

## Introduction

Filters are used to format the data in the view. They can be used in the following way:

```html
{{ expression | filter }}
```

Where `expression` is the data to be formatted and `filter` is the name of the filter.



## BMML Time
For a time string, this filter will format the time to the following format: `H:mm A`
By default the format is `H:mm a`, but you can specify a different format by passing it as a parameter to the filter.
For example:
```html
{{ '12:00:00' | bmmlTime }}
```
Or with a different format:
```html
{{ '12:00:00' | bmmlTime: 'HH:mm' }}
```

Read more about the [Format tokens](https://momentjs.com/docs/#/displaying/format/) for the format options.