# Custom Script Modules Usage Guide

This document outlines how to use the built-in modules when writing custom scripts. You can use any of the following modules in your script by referencing them via their respective variable names. Each module provides different functionality to streamline and empower your scripting experience.

---
> ⚠️ **Warning**  
> Improper, malicious, or irresponsible use of these modules — including unauthorized data access, manipulation, or exploitation — may result in **immediate account suspension** and **permanent loss of access**.  
> All actions are logged and reviewed. Use with integrity.
---

## Database (`db`)

Provides access to all database operations.

### Common Methods
- `db.query(queryString, values?, options?)`
- `db.transaction(async (trx) => { ... })`
- `db.create(table, data, options?)`
- `db.read(table, filter?, order?, columns?, options?)`
- `db.readOne(table, filter?, order?, columns?, options?)`
- `db.update(table, query, values, options?)`
- `db.delete(table, id, options?)`
- `db.count(table, key, filter?, options?)`
- `db.getMax(table, column, filter?, options?)`

Refer to the function names for their expected inputs and outputs.

### Examples
```js
const result = await db.read("users", { role: "admin" });

await db.transaction(async (trx) => {
  await db.create("orders", { item: "A" }, { trx });
});
```

---

## Axios (`axios`)

Use for making HTTP requests.

### Example
```js
const response = await axios.get('https://api.example.com/data');
```

Supports all standard Axios methods: `get`, `post`, `put`, `delete`, etc.

---

## Lodash (`_`)

Use Lodash for data manipulation and utility functions.

### Example
```js
const ids = _.map(records, 'id');
```

---

## Moment (`moment`)

Use Moment to format and manipulate dates.

### Example
```js
const today = moment().format('YYYY-MM-DD');
```

---

## Call Script (`callScript`)

Call another script by name and pass environment data.

### Example
```js
const result = await callScript('script_name', { key: 'value' });
```

Returns a promise that resolves to the other script's return value.

---

## Call Report (`callReport`)

Call a report by its ID and pass parameters.

### Example
```js
const rows = await callReport('report_id', { param1: 'value' });
```

Returns an array of rows from the report.

---

## Field Helper (`fieldHelper`)

### Get a single field definition:
```js
const field = await fieldHelper.getFieldPerTable('table_name', 'field_name');
```

### Get all field definitions:
```js
const fields = await fieldHelper.getFieldsPerTable('table_name', { expand: true });
```

Useful when you need metadata or rules for dynamic fields.

---

## PDF Helper (`pdfHelper`)

Generate PDFs from a document definition.

### Example
```js
const buffer = await pdfHelper.generatePdf(docDefinition);
```

You can also stream the document:
```js
const stream = pdfHelper.generatePdf(docDefinition, options, true);
```

---

## Save File Helper (`saveFileHelper`)

### Save a PDF buffer:
```js
const fileId = await saveFileHelper.save('filename.pdf', buffer, 'table', table_id, user_id);
```

### Upload a file manually:
```js
await saveFileHelper.uploadFile({ table_name, table_id, folder_id }, req.query, req.file, req.body, 'internalName', user);
```

Other utility methods include:
- `recordFile(...)`
- `pasteFile(...)`
- `mkdirIfNotExists(...)`
- `selectDestination(...)`
- `getRelative(...)`
- `getInternalName(...)`

---

Use these modules responsibly and ensure proper error handling in your scripts. Only interact with exposed methods as documented above.

