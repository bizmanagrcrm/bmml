# Bizmanage Server Side Scripts

## Introduction
BizmanageCRM allows you to write custom server-side scripts that can be executed when a specific event occurs.
Currently, you can execute custom server-side scripts in the following ways:
- HTTP Request:
    the script will be executed when an HTTP request is received by the server at the specified endpoint:
        ```/scripts/run/{{scriptName}}``` - for authenticated requests, and
        ```/public/script/{{scriptName}}/{{token}}``` - for public requests.
- Scheduled Task:
    the script will be executed at the specified time interval, tasks are scheduled by specifying a valid **Cron Job**, for more info and to generate a **Cron Job** [click here](http://www.cronmaker.com/).
    (note: this is not the **Linux cron system**, rather the [**node-cron**](https://www.npmjs.com/package/node-cron) system)


## How to create a server-side script
To create a server-side script, follow these steps:
1. Go to the Admin Portal.
2. Click on the "Backend Scripts" tab.
3. Click on the "Create Script" button, and fill out the scripts metadata.
   - Enter the **script name**.
   - Enter the scripts HTTP Method (GET or POST, and this doesn't have any effect yet).
   - Select if the script should be **active**. (if off, it will not run even if you schedule or HTTP call it)
   - Select which **modules to import**, to use within the script.
   - Customize a **timeout** till when the script should run, once it passes this time, the script will be killed. (defaults to 30 seconds)
   - Select if the script should be **accessible publicly**, if yes, a token will be generated, which will let you use the script as a webhook.
   - Select if the script should run on a **schedule**, if yes, specify a schedule from the predefined options, or write a custom Cron Job.
   - **Save** the script.
7. Write the script code.
8. Click on the "Save" button.

## Available Actions
1. **Edit Script Metadata**: Edit the script metadata as specified above.
2. **Edit Script Code**: Edit the underlying Js code for the script.
3. **Regenerate Token**: If the script is public, use this action to generate a new token and expire the old token for the script.
4. **Run Script**: This action will launch a new tab with the url for the script, executing it via HTTP.
5. **Delete Script**: Use this action to delete a script.
6. **Script Run Logs**: This will open a modal, with the scripts run logs, and overall script info.

## How to write a script?
You can write server-side scripts in JavaScript. The script code should be valid Node.js code that can be executed by the server.

## Available Objects
The following objects are available in the server-side scripts:
- user: the user object that triggered the script. This object contains the user data. and ip address.
- query: the query object that contains the query parameters of the request.
- body: the body object that contains the body of the request. (for POST requests)
- imported modules: all the imported modules are available to use in the script, 
    for example if you include the Database module, you can use it by writing ```db.read(/*query*/)``` in the script.
