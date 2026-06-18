# Reports Settings

The **settings box** allows customizing the columns in your reports and configuring the right click menu.

## Attributes

- **`clms`** — array of column definitions.
- **`actions`** — configuration object that defines the view the menu is taken from and menus.
- **`csv`** - download configuration

### Column Object Properties

| Property | Type | Description |
|----------|------|-------------|
| `name` | `string` | Column name. |
| `showColumnFooter` | `boolean` | Set to `true` to display a footer. |
| `agg` | `string` | Footer calculation / aggregation (`sum`, `currency` etc.). |
| `format` | `string` | Display format for column and footer (`currency`, `number` etc.). |

### Example

```json
{
  "clms": [
    {
      "name": "Invoice Amount",
      "showColumnFooter": true,
      "agg": "currency",
      "format": "currency"
    },
    {
      "name": "# of Valid Units",
      "showColumnFooter": true,
      "agg": "sum"
    }
  ]
}
```

## `actions` Attribute

The `actions` setting controls which action menus are available for the report from a specific view.


### Actions Object Properties

| Property | Type | Description |
|----------|------|-------------|
| `view_name` | `string` | The name of the view where the actions come from. |
| `menus` | `array` | List of action menu definitions from in this view that you want on the right click menu. |

### Menu Object Properties

| Property | Type | Description |
|----------|------|-------------|
| `internal_name` | `string` | Internal identifier of the action to display. |

### Example

```json
"actions": {
  "view_name": "projects",
  "menus": [
    {
      "internal_name": "edit"
    },
    {
      "internal_name": "dashboard"
    }
  ]
}

```
## `csv` Attribute

The csv attribute configures the downloaded CSV file. 

### Actions Object Properties
| Property | Type | Description |
|----------|------|-------------|
| `file_name` | `string` | The name of the file once downloaded. this is optional - will use default name if not set |


### Available Dynamic Values

The `file_name` supports dynamic placeholders using `${...}` syntax.

#### `NOW`

Use `${NOW}` to insert the current date.

```json
{
  "csv": {
    "file_name": "P_${NOW}_DAF"
  }
}
```

Example output:

```text
P_2026-06-18_DAF.csv
```

#### `DATETIME`

Use `${DATETIME}` to insert the current date and time.

```json
{
  "csv": {
    "file_name": "P_${DATETIME}_DAF"
  }
}
```

Example output:

```text
P_2026-06-18_14_30_22_DAF.csv
```

`DATETIME` is useful when the same report may be downloaded multiple times in one day and each file should have a unique name.

### Using Report Params in the File Name

Report params can also be used in the file name. Use the param’s `internal_name` inside `${...}`.


# Reports Params
---

## `params` Attribute

The **params box** defines the input parameters required to run a report.

Each parameter becomes an input field in the report UI and is passed into the SQL query using named bindings.

Parameters are referenced in SQL using:

*:param_name*


Example:

```sql
WHERE l.project__c = :project
AND cr.report_year__c = :year
AND cr.report_month__c = :month
```

## Structure

`params` is an array of parameter definitions.

### Parameter Object Properties

| Property | Type | Description |
|----------|------|-------------|
| `display_name` | string | Label shown in the report UI. |
| `internal_name` | string | Parameter name used in SQL (referenced as `:internal_name`). |
| `input_type` | string | Type of input field (`number`, `text`, `ref`). |
| `required` | boolean | If `true`, the report cannot run without this value. |
| `otherTable` | string | *(For `ref` type only)* Table used to populate the reference list. |
| `otherColumnDisplay` | string | *(For `ref` type only)* Column displayed in the dropdown. |

---

### Input Types

#### `number`
Numeric input field.

#### `text`
Free text input field.

#### `ref`
Reference selector (dropdown) populated from another table.

**Requires:**
- `otherTable`
- `otherColumnDisplay`


## Example

```json
[
  {
    "display_name": "Customer",
    "input_type": "ref",
    "otherColumnDisplay": "name",
    "otherTable": "customers",
    "required": true,
    "internal_name": "customer"
  },
  {
    "display_name": "Year",
    "input_type": "number",
    "required": true,
    "internal_name": "year"
  },
  {
    "display_name": "Month",
    "input_type": "text",
    "required": true,
    "internal_name": "month"
  }
]
```
Used in SQL:
```sql
WHERE l.customer__c = :customer
AND cr.report_year__c = :year
AND cr.report_month__c = :month
```


