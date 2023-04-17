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

The following variables are supported:
- to - email address of the recipient
- subject - email subject
- message - email message
- title - title of the popup (default: Send Email)
- template_id - id of the email template to use (optional)
- log_table - table name to relate the log to (optional)
- log_id - id of the record to relate the log to (optional)