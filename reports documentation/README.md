# Reports Settings

The **settings box** allows customizing the columns in your reports and configuring the right click menu.

## Attributes

- **`clms`** — array of column definitions.
- **`actions`** — configuration object that defines the view the menu is taken from and menus.

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


