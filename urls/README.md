# BMML urls


## Introduction

At BizmanageCRM we allow you to write custom urls that will be embeded in the system.

## Internal urls

Internal urls are urls that are managed by the system. They are used to redirect the user to a specific page, using the url. (Note, this is internal routing, not a full page reload)

An internal url will typically start with a `/#` and will be followed by the page url.


Example:
```/#/home```


Note, you can use {{}} to bind the url to a variable. For example:
```/#/customer/{{customerId}}```

Variables can be passed to the page using the query string. For example:
```/#/customer/{{customerId}}?name={{customerName}}```

## Email

To create a url that will open the send-email popup, use the following syntax:
```/#/open-email?to={{email}}&subject={{subject}}&message={{message}}```

The following query values are supported:
- from - email address of the sender (optional - default: current user/employee email)
- to - email address of the recipient
- cc - email address of the cc recipient (optional)
- bcc - email address of the bcc recipient (optional)
- subject - email subject
- message - email message
- title - title of the popup (default: Send Email)
- template_id - id of the email template to use (optional)
- log_table - table name to relate the log to (optional)
- log_id - id of the record to relate the log to (optional)
- model_name - the name of the model (view) that should be used for parsing the template
- model_id - the id of the model (view) that should be used for parsing the template
- auto_send - if true, the email will be sent automatically once all required fields are filled (optional - default: false)
- on_sent_go_to - url to redirect to after the email is sent (optional) the url is going to be parsed for variables with the email response (more details required) and the rest of the params of the original url. for example {{params.log_id}} is going to be replaced with the log_id.

## Form

To open a form to create a new record, use the following syntax:
```/#/add/{{InternalViewName}}```

To open a form to edit an existing record, use the following syntax:
```/#/update/{{InternalViewName}}?id={{recordId}}```

The following query values are supported:

- id - id of the record to edit (optional - default: new record)
- title - title of the popup (default: Add {{InternalViewName}})
- pre_data - json object with data to be eventually submitted with the form - this will override the form inputs and will work even for fields that are not displayed in the form (optional) - it will also hide the field from the form.
- initial - json object with data to prefill the form with (optional)
- pre_data_{{fieldName}} - this is equivalent to pre_data but for the field {{fieldName}} (optional)
- initial_{{fieldName}} - this is equivalent to initial but for the field {{fieldName}} (optional)