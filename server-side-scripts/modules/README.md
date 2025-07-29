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

## Quotes Helper (`quotesHelper`)

The `quotesHelper` module exposes core functionality for creating and saving quotes. It combines utilities from the internal quote management system.

### API

#### Create Methods

* `quotesHelper.create.quote(data, user?)`
* `quotesHelper.create.unit(data, user?)`
* `quotesHelper.create.default(data)`

#### Save Methods

* `quotesHelper.save.saveQuote(quote, timestamp, user)`
* `quotesHelper.save.createUpdateQtItem(item, user, trx?, keepLink?)`
* `quotesHelper.save.createUpdateQtItems(quote, items, user)`
* `quotesHelper.save.applyMarkup(quote, markup, user, trx?)`
* `quotesHelper.save.reorderItems(quote, data, user)`
* `quotesHelper.save.quickEnter(quote, items, query, user)`
* `quotesHelper.save.deleteQtItems(ids, keepLink, user)`
* `quotesHelper.save.changeListPrice(data, user)`
* `quotesHelper.save.getAllLinkedItems(item, quote_root_id)`
* `quotesHelper.save.getAllLinkedQuotes(root_id)`

---

### Examples

#### Create a new quote

```js
const quote = await quotesHelper.create.quote({ name: "Test", project: 12 }, user);
```

#### Save an updated quote

```js
await quotesHelper.save.saveQuote(quoteData, Date.now(), user);
```

All actions within `quotesHelper` interact with system-managed `quotes`, `quote_items`, `quote_defaults`, and related tables. Use responsibly and ensure data consistency across calls


---

## Projects Helper (`projectsHelper`)

Provides utility functions for managing project-related workflows, including project creation, PO handling, dashboard data aggregation, and status updates.

### Common Methods

- `projectsHelper.createPO(projectId, user, po_number)`
- `projectsHelper.removePO(projectId, user)`
- `projectsHelper.getDashboard(userId)`
- `projectsHelper.getProject(id, extended?, user?)`
- `projectsHelper.getProjects(query, countOnly?)`
- `projectsHelper.completeProject(id, query, user)`
- `projectsHelper.markTask(id, query, user)`
- `projectsHelper.autoGenerateProposal(id, user)`
- `projectsHelper.addUpdateProject(project, user, query?, options?)`
- `projectsHelper.completeProjects(projects, user)`
- `projectsHelper.makeQtFinal(quote_id, user)`
- `projectsHelper.startEnd(id, type, open_tasks, user, options?)`
- `projectsHelper.getAllAssignedPerProject(projectId, compact?)`

### Example

```js
await projectsHelper.createPO(12, currentUser, 3021);

const dashboard = await projectsHelper.getDashboard(currentUser.id);

const project = await projectsHelper.getProject(12, true, currentUser);
```

---
## Mail Helper (`mailHelper`)

Provides email-related functionality, including sending messages, using templates, handling unlock requests, and logging.

### Common Methods

- `mailHelper.send(mailOptions)`
- `mailHelper.sendGeneric(data, user)`
- `mailHelper.sendMsg(user_id, msg, email?)`
- `mailHelper.sendTemplate(fileName, data, options?)`
- `mailHelper.sendWithEmailTemplate(to, template_name, models, options?)`
- `mailHelper.requestUnlock(file, user)`
- `mailHelper.getAll()`
- `mailHelper.getEmailLog()`

### Example

```js
await mailHelper.send({
  to: 'admin@example.com',
  subject: 'Test Email',
  html: '<p>Hello World</p>',
  from: 'noreply@example.com'
});

await mailHelper.sendWithEmailTemplate(
  'user@example.com',
  'welcome_template',
  { username: 'John' },
  { subject: 'Welcome!', from: 'support@example.com' }
);
```


---

## Schedule Script Execution (`scheduleScriptExecution`)

Schedule the execution of custom backend scripts.

### Example
```js
scheduleScriptExecution(script_name, {after_ms, data: {some_data: 123}}, user);
```

Returns the `MessageQueue` Object created when the task was scheduled.

---

## Proposal Helper (`proposalHelper`)

Handles proposals, invoices, quote rendering, emailing, approval, and related operations. Useful for creating customer-facing documents based on project quotes.

### Common Methods

- `proposalHelper.generate(project, { settings, payment_plan, quote_id, approved })`
- `proposalHelper.updateSettings(id, data)`
- `proposalHelper.getInfo(projectId, quoteId)`
- `proposalHelper.email(id, data, user)`
- `proposalHelper.getRenderData(Proposal)`
- `proposalHelper.copy(id)`
- `proposalHelper.getById(id)`
- `proposalHelper.cancelInvoice(id)`
- `proposalHelper.approve(url, body, user)`
- `proposalHelper.renderInvoice(invoice_id, user)`
- `proposalHelper.createInvoice(proposal)`
- `proposalHelper.expressInvoice(data, user)`
- `proposalHelper.customerInvoice(invoiceData, user)`
- `proposalHelper.proposalApproved(proposal, user, invoice, quote)`
- `proposalHelper.recalculateInvoiceAmount(invoiceId)`

### Example

```js
await proposalHelper.email(42, {
  to: 'client@example.com',
  subject: 'Proposal Document',
  message: 'Attached is your proposal',
  from: 'sales@company.com',
  include_attachment: true
}, user);

const proposal = await proposalHelper.generate(33, {
  settings: { /* template settings */ },
  quote_id: 89,
  approved: true
});

await proposalHelper.approve('abc123', {
  quote_id: 89,
  signature_name: 'Jane Doe',
  signature_font: 'Helvetica',
  items_approved: true
}, user);
```

---


Use these modules responsibly and ensure proper error handling in your scripts. Only interact with exposed methods as documented above.

