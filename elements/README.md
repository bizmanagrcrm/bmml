# BMML Elements


### `<bmml-report>`
This element is used to embed a report in the page. The report is identified by its id.
example:
```<bmml-report id="1"></bmml-report>```
Supported attributes:
- `id` - the id of the report to embed
- `auto-execute` - if this attribute is set to true, the report will be executed automatically when the page is loaded. (default: false) - the system will attempt to load the report whenever there is a change in the report parameters.
- ... all report parameters names could be used as attributes. For example, if the report has a parameter named `name`, you can use the `name` attribute to set the value of the parameter. (Note, you can use variables in the attributes, for example: `name="{{$urlParams.name}}"`)

#### Note
, You cannot use underscores or dashes in the param internal name. For example, if the param internal name is `first_name`, you should change it to `firstName`, and then you can use the `first-name` attribute to set the value of the parameter.


### `<bmml-form>`
This element is used to embed a form in the page. The form is the view name and the form name.

example:
```<bmml-form table-name="customers" form-name="default"></bmml-form>```

- `table-name` - the name of the table (view) of the form
- `form-name` - the name of the form (optional - default: "default")
- `action` - the action of the form (required) - the following actions are supported:
    - `add` - add a new record
    - `update` - update a record
    - `duplicate` - duplicate a record
- `id` - the id of the record to edit (optional - default: new record)
- `title` - title of the popup (default: Add/Edit {{ViewName}})



### `<bmml-data-src>`
This element is used to embed a data source in the page. The data source is identified by the following attributes:

- `source-url` - the url of the data source - if this is specified, the data source will be loaded from the url.
- `type` - the type of the data source - The following types are currently supported
    - `dashboard` - a dashboard data source, (with this type, you must specify the `src-name` and `src-id` attributes. src-name is for the dashboard name and src-id is for the record id of the dashboard)
    - `crud` - a crud data source, (with this type, you must specify the `view-name` and `op` attributes. view-name is for the view name and op is for the operation name)

- `method` - the method to use to load the data source (default: GET) - this attribute is used only if the `source-url` attribute is specified. and not used if the `type` attribute is specified.

- `param-{{param-name}}` - the parameters of the data source. You can use this attribute multiple times to specify multiple parameters. For example: `param-name="value"` - this will add a parameter named `name` with the value `value`.

- `header-{{header-name}}` - the headers of the data source. You can use this attribute multiple times to specify multiple headers. For example: `header-name="value"` - this will add a header named `name` with the value `value`.

- `payload-{{payload-name}}` - the payload of the data source. You can use this attribute multiple times to specify multiple payload fields. For example: `payload-name="value"` - this will add a payload field named `name` with the value `value`.

- `payload` - the payload of the data source. This attribute is used only if the `source-url` attribute is specified. and not used if the `type` attribute is specified.

- `params` - the parameters of the data source. This attribute is used only if the `source-url` attribute is specified. and not used if the `type` attribute is specified.

- `headers` - the headers of the data source. This attribute is used only if the `source-url` attribute is specified. and not used if the `type` attribute is specified.
  
- `broadcast` -A string value that the system listens for. When this broadcast is detected, the system reloads the BMML data. This attribute is optional.

- `scope-data-var` - The name of the variable that will hold the data source result. Default is `$data`.




The following attributes are used for `type=dashboard`:

- `src-name` - the internal name of the data source.
- `src-id` - the id of the data source.

- `load-sections` - for type=dashboard, this attribute specifies a list of sections to load. The sections are separated by commas. For example: `load-sections="section1,section2,section3"`

- `sections-as-object` for type=dashboard, if set as true, the sections will be loaded as an object.

    An example of a data source element:
    ```<bmml-data-src type="dashboard" src-name="customers" src-id="1"></bmml-data-src>```

    Of course, you can use variables in the attributes, for example:
    ```<bmml-data-src type="dashboard" src-name="{{$urlParams.name}}" src-id="{{$urlParams.id}}"></bmml-data-src>```

    This example will load the data source based on the url parameters.

The following attributes are used for `type=crud`:
    
- `view-name` - the internal name of the view.
- `op` - the operation name (optional - default: list)
    
        An example of a data source element:
        ```<bmml-data-src type="crud" view-name="customers" op="read"></bmml-data-src>```
    
        Of course, you can use variables in the attributes, for example:
        ```<bmml-data-src type="crud" view-name="{{$urlParams.name}}" op="{{$urlParams.op}}"></bmml-data-src>```

The variables that can be used in the children of this element are:

#### `$data` variable (with type = 'dashboard')
Note the var name could be changed using the `scope-data-var` attribute.
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

#### Example with nested elements
```<bmml-data-src type="dashboard" src-name="customers" src-id="1">
    <bmml-data-src ource-url="/cust_report/query/88" param-customer="{{$urlParams.id}}" scope-data-var="reportData">
        <div ng-if="!$loading">
            <div>Report Data:</div>
            <div>{{reportData.data}}</div>
        </div>
        <div ng-if="$loading">
            Loading report...
        </div>
        <div ng-if="$error">
            {{$errorMessage}}
        </div>
    </bmml-data-src>
</bmml-data-src>```
