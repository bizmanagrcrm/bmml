# BizmanageCRM Custom Scripts for actions

## Introduction

At BizmanageCRM we allow you to write custom javascript code that can be attached to an action and executed when the action is triggered.

## what is an action?
A custom action is a trigger that can be added to the system. When the trigger is activated, the system will execute the custom code that is attached to the action.
It can be in the form of a button, a link, a menu item, or any other trigger that can be added to the system.

## BMML action environment
An action is always attached to a bizmznage view, and one or multiple records.



### Record Object
A variable named `record` is available in the action code. This variable contains the data of the record that triggered the action. (it could be the row that was selected, or the form data that was submitted)

### $http
the `$http` service is available in the action code. You can use it to send requests to the server.
see angularjs documentation for more information. https://docs.angularjs.org/api/ng/service/$http

### $q
the `$q` service is available in the action code. You can use it to create promises.
see angularjs documentation for more information. https://docs.angularjs.org/api/ng/service/$q
