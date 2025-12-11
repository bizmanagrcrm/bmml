# BMML Forms

## Introduction
In BizmanageCRM, forms are used to create, edit, and duplicate records.
A Form is always associated with a specific view (model) and is used to create, edit, or duplicate records of that view.
In the Admin Portal, you can create and manage forms for each view.
You can have multiple forms for the same view, each with different fields and settings.


### How to open a form
To open a form to create a new record, use the following syntax:
```/#/add/{{InternalViewName}}```

Replace `{{InternalViewName}}` with the internal name of the view (model) you want to create a record for.

To open a form to edit an existing record, use the following syntax:
```/#/update/{{InternalViewName}}?id={{recordId}}```

Replace `{{InternalViewName}}` with the internal name of the view (model) you want to edit a record for, and `{{recordId}}` with the id of the record you want to edit.


To open a form to duplicate an existing record, use the following syntax:
```/#/duplicate/{{InternalViewName}}?id={{recordId}}```

Replace `{{InternalViewName}}` with the internal name of the view (model) you want to duplicate a record for, and `{{recordId}}` with the id of the record you want to duplicate.


### How to preset form fields with values?

You can preset form fields with values by adding query parameters to the form url.

There are two ways to preset form fields with values:
1. Using pre_data
2. Using initial

#### Using pre_data
You can preset form fields with values by adding a `pre_data` query parameter to the form url.
You can use pre_data={{json}} to preset multiple fields with values.
Or, alternatively, you can use pre_data_{{fieldName}}={{value}} to preset a single field with a value.

We recommend using the `pre_data_{{fieldName}}` method to preset form fields with values, as it is more flexible and allows you to preset multiple fields with values.

Please note that `pre_data` will override the form inputs and will work even for fields that are not displayed in the form. It will also hide the field from the form.

If you use that with an update or duplicate form, the fields will be updated with the new values, even if they are not displayed in the form.

#### Using initial
You can preset form fields with values by adding an `initial` query parameter to the form url.
You can use initial={{json}} to preset multiple fields with values.
Or, alternatively, you can use initial_{{fieldName}}={{value}} to preset a single field with a value.

We recommend using the `initial_{{fieldName}}` method to preset form fields with values, as it is more flexible and allows you to preset multiple fields with values.

Please note that `initial` will prefill the form with the values, but it will not hide the fields from the form.

If you use that with an update or duplicate form, the fields will be prefilled with the new values, you will not see the current values in the form, you will see the new values defined in the initial parameter.



## Custom HTML In Forms

You can add custom HTML to the form via the admin portal. The custom HTML will be displayed in the form at the specified location in the form layout.

In the html you can also use variables, for example:
```html
<div>
    <h1>MY CUSTOM HTML</h1>
    <p>{{record.name}}</p>
    <input type="text" ng-model="record.custom_field">
</div>
```

The `record` variable is the record object that is being edited or created in the form.

## Charge Credit Card Form
To open the charge cc form, redirect to the following url: /#/payments/charge-cc

The following query parameters can be sent along: 
* amount: will prefill the amount input
* pre_data_amount: will prefill amount input AND disable the input box. If both amount and pre_data_amount is sent, pre_data_amount will override amount.
* gateway: will prefill the gateway
* customer: the customer to connect the cc charge to
* invoice: the invoice to apply the charge to

Example: /#/payments/charge-cc?pre_data_amount={{pledge_amount}}&customer={{cust_id}}&gateway=1
