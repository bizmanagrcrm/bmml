# BMML Elements


### `<bmml-report>`
This element is used to embed a report in the page. The report is identified by its id.
example:
```<bmml-report id="1"></bmml-report>```

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