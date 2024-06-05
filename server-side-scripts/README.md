# Bizmanage Server Side Scripts

## Introduction
BizmanageCRM allows you to write custom server-side scripts that can be executed when a specific event occurs.
Currently, you can write custom server-side scripts for the following events:
- HTTP Request:
    the script will be executed when an HTTP request is received by the server at the specified endpoint:
        /scripts/run/{{scriptName}} - for authenticated requests
        /public/script/{{scriptName}}/{{token}} - for public requests
- Scheduled Task:
    the script will be executed at the specified time interval.


## How to create a server-side script
To create a server-side script, follow these steps:
1. Go to the Admin Portal.
2. Click on the "Server Side Scripts" tab.
3. Click on the "New Script" button.
4. Enter the script name.
5. Select the script type (HTTP Request or Scheduled Task).
6. Write the script code.
7. Click on the "Save" button.

### How to write a script?
You can write server-side scripts in JavaScript. The script code should be a valid JavaScript code that can be executed by the server.

### Available Objects
The following objects are available in the server-side scripts:
- user: the user object that triggered the script. This object contains the user data. and ip address.
- query: the query object that contains the query parameters of the request.
- body: the body object that contains the body of the request. (for POST requests)