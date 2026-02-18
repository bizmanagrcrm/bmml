# Reports Settings

The **settings box** allows customizing the columns in your reports.

## Attributes

- **`clms`** — array of column definitions.

### Column Object Properties

| Property | Type | Description |
|----------|------|-------------|
| `name` | `string` | Column name. |
| `showColumnFooter` | `boolean` | Set to `true` to display a footer. |
| `agg` | `string` | Footer calculation / aggregation (`sum`, `currency`, `average`, etc.). |
| `format` | `string` | Display format for column and footer (`currency`, `number`, `percent`, `date`, etc.). |

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
