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
