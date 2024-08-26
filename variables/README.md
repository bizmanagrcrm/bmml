# BMML Variables


## Introduction
At BizmanageCRM we allow you to write custom code that will be embeded in the system.
There are some variables that you can have access to in your custom code.


## BMML Variables

### {{$urlParams}}
This is an object that contains the url parameters. For example, if the url is `/#/page/123?name=John&code=abc`, then the ```$urlParams``` object will be:
```json
{
    "_url" : "123", //this is the page url
    "name": "John",
    "code": "abc"
}
```

## Date and Time Variables

### {{$now}}
This is a date object that contains the current date and time.

Can be used to format the date in the following way:
```javascript
{{$now | date: 'yyyy-MM-dd HH:mm:ss'}}
```

### {{$toDate()}}
This is a function that can be used to convert a string to a date object. The function has the following signature:
```javascript
{{$toDate('2020-01-01 12:00:00') | date: 'yyyy-MM-dd HH:mm:ss'}}
```
This can be use in conjunction with the ```$now``` variable to calculate the difference between two dates.
Example:
```javascript
{{$toDate('2020-01-01 12:00:00') - $now}}
```

### {{moment()}}
This gives you access to the entire moment.js library.

See the documentation at https://momentjs.com/
