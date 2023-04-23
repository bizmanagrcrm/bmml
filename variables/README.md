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