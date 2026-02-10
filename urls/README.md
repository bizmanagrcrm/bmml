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
```/#/open-email?to={{email}}&subject={{subject}}&message={{message}}&hide_fields=to&hide_fields=from```

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
- batch_mode - open the popup in batch mode - this will send multiple emails to multiple recipents, and will not show the template interpolation. **Note:** when using batch mode, you can only use one view in variables.
- main_recipient - email address to use as the main recipient (to) in batch mode. When set, this email address will be used as the "to" and all other recipients will be added as bcc. (optional - only applies to batch mode)
- email_field - the name of the field that contains the email address (optional - default: email) this is used to match the recipient email address with the field in the view for batch mode and for parsing the template
- override_send_action - internal name of a custom action on the *cust_templates* table that will run instead of the default *send email* action
- $modal_size - size of the popup (optional - default: lg) - possible values: sm, md, lg
- hide_fields - name of fields to hide on the popup (optional). Available fields: template, from, to, message, subject
- post_send_action - internal name of a custom action on the *cust_templates* table that will run **after** the default *send email* action


## SMS

To create a url that will open the send-sms popup, use the following syntax:

```/#/open-sms?to={{phone}}&message={{message}}```

URL with all features put to use:

```/open-sms/{{to_phone}}?from={{system_phone || gateway_id}}&model_name=customers&model_id={{id}}&log_table=customers&log_id={{id}}&template_id=5&hide_fields=to&hide_fields=from```

The following query values are supported:
- from - SMS gateway ID of the sender or Gateway Phone Number
- to - phone number of the recipient
- message - sms message
- title - title of the popup (default: Send SMS)
- template_id - id of the sms template to use (optional)
- log_table - table name to relate the log to (optional)
- log_id - id of the record to relate the log to (optional)
- model_name - the name of the model (view) that should be used for parsing the template
- model_id - the id of the model (view) that should be used for parsing the template
- auto_send - if true, the sms will be sent automatically once all required fields are filled (optional - default: false)
- on_sent_go_to - url to redirect to after the sms is sent (optional) the url is going to be parsed for variables with the sms response (more details required) and the rest of the params of the original url. for example {{params.log_id}} is going to be replaced with the log_id.
- override_send_action - internal name of a custom action on the *cust_templates* table that will run instead of the default *send sms* action
- $modal_size - size of the popup (optional - default: lg) - possible values: sm, md, lg
- hide_fields - name of fields to hide on the popup (optional). Available fields: template, from, to, message.
- post_send_action - internal name of a custom action on the *cust_templates* table that will run **after** the default *send sms* action


## Refunds
To create a url that will open the refund form, use the following syntax:
```#/payments/refund/{{id}}?post_refund_action=test_refund_action__c```

- The id is the id of the transaction being refunded

The following query values are supported:
- post_refund_action - internal name of a custom action on the *payment_transaction* table that will run **after** the refund is proccessed

## Form

To open a form to create a new record, use the following syntax:
```/#/add/{{InternalViewName}}```

To open a form to edit an existing record, use the following syntax:
```/#/update/{{InternalViewName}}?id={{recordId}}```

To open a form to duplicate an existing record, use the following syntax:
```/#/duplicate/{{InternalViewName}}?id={{recordId}}```

The following query values are supported:

- id - id of the record to edit (optional - default: new record)
- title - title of the popup (default: Add {{InternalViewName}})
- pre_data - json object with data to be eventually submitted with the form - this will override the form inputs and will work even for fields that are not displayed in the form (optional) - it will also hide the field from the form.
- initial - json object with data to prefill the form with (optional)
- pre_data_{{fieldName}} - this is equivalent to pre_data but for the field {{fieldName}} (optional)
- initial_{{fieldName}} - this is equivalent to initial but for the field {{fieldName}} (optional)
- $modal_size - size of the popup (optional - default: lg) - possible values: sm, md, lg
- form_name - the name of the form to use (optional - default: default)
- active_tab - the index of the active tab, starting from 1 (optional - default: 1)


To read more about the form url, please visit the [BMML Forms](https://github.com/bizmanagrcrm/bmml/blob/main/forms/README.md)
