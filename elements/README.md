# BMML Elements


### `<bmml-report>`
This element is used to embed a report in the page. The report is identified by its id.
example:
```<bmml-report id="1"></bmml-report>```
Supported attributes:
- `id` - the id of the report to embed
- `auto-execute` - if this attribute is set to true, the report will be executed automatically when the page is loaded. (default: false) - the system will attempt to load the report whenever there is a change in the report parameters.
- ... all report parameters names could be used as attributes. For example, if the report has a parameter named `name`, you can use the `name` attribute to set the value of the parameter. (Note, you can use variables in the attributes, for example: `name="{{$urlParams.name}}"`)


### `<bmml-form>`
This element is used to embed a form in the page. The form is the view name and the form name.

example:
```<bmml-form table-name="customers" form-name="default"></bmml-form>```

- `table-name` - the name of the table (view) of the form
- `form-name` - the name of the form (optional - default: "default")
- `id` - the id of the record to edit (optional - default: new record)
- `title` - title of the popup (default: Add/Edit {{ViewName}})



### `<bmml-data-src>`
This element is used to embed a data source in the page. The data source is identified by the following attributes:

- `source-url` - the url of the data source - if this is specified, the data source will be loaded from the url.
- `type` - the type of the data source - The following types are currently supported
    - `dashboard` - a dashboard data source, (with this type, you must specify the `src-name` and `src-id` attributes. src-name is for the dashboard name and src-id is for the record id of the dashboard)

- `src-name` - the internal name of the data source.
- `src-id` - the id of the data source.

An example of a data source element:
```<bmml-data-src type="dashboard" src-name="customers" src-id="1"></bmml-data-src>```

Of course, you can use variables in the attributes, for example:
```<bmml-data-src type="dashboard" src-name="{{$urlParams.name}}" src-id="{{$urlParams.id}}"></bmml-data-src>```

This example will load the data source based on the url parameters.

The variables that can be used in the children of this element are:

#### `$data` variable (with type `dashboard``)
This variable contains the data of the data source. It is an object with the following properties:
    `data` - the data of the data source (this is an object with the fields of the data source)
    `display_name` - the display name of the data source
    `...` - other properties

#### `$error` variable (boolean)
This variable is true if there was an error loading the data source.

#### `$errorMessage` variable (string)
This variable contains the error message if there was an error loading the data source.

#### `$loading` variable (boolean)
This variable is true if the data source is still loading.

#### Example
    ```<bmml-data-src type="dashboard" src-name="{{$urlParams.name}}" src-id="{{$urlParams.id}}">
        <div ng-if="!$loading">
            <div>{{$data.display_name}}</div>
            <div>{{$data.data.name}}</div>
        </div>
        <div ng-if="$loading">
            Loading...
        </div>
        <div ng-if="$error">
            {{$errorMessage}}
        </div>
    </bmml-data-src>``` 