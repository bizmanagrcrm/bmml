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

## Cheerio HTML Parser (`cheerio`)

Use Cheerio to parse and manipulate HTNL.

### Example
```js
const html = cheerio.load("<div id='test'>hello</div>");
return html("#test").text();
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

## Project Status Helper (`statusHelper`)

Manages project status workflows, including updating project states, handling tasks, recalculating due dates, and notifying employees.

### Common Methods

- `statusHelper.createUpdate(status)`
- `statusHelper.updateProjectStatus(project, status, user, query?)`
- `statusHelper.findNextProjectStatus(project, project_status_id?)`
- `statusHelper.handleOpenTasks(project, open_tasks?)`
- `statusHelper.updateDueDateProject(project, ps, user)`
- `statusHelper.applyNextStatusByTask(task, project, user, next_project_status?)`
- `statusHelper.isAllToBeCompleted(project_status, taskId)`

### Example

```js
// Update project to a new status
await statusHelper.updateProjectStatus(12, 5, currentUser, {
  open_tasks: "complete"
});

// Handle open tasks for a project
await statusHelper.handleOpenTasks(12, "cancel");

// Find the next project status
const nextStatus = await statusHelper.findNextProjectStatus(12);

// Recalculate due dates for a project
await statusHelper.updateDueDateProject(project, currentProjectStatus, currentUser);

// Move project to next status based on task completion
await statusHelper.applyNextStatusByTask(task, project, currentUser);

// Check if all tasks for a status are completed (except a given task)
const allCompleted = await statusHelper.isAllToBeCompleted(statusId, taskId);
```

---

## Payments Helper (`paymentsHelper`)

Provides functions for managing payments, gateways, balance sheets, and payment methods, including charging credit cards, importing/saving payment methods, and retrieving payments for invoices.

### Common Methods

- `paymentHelper.chargeCC(data, user)`
- `paymentHelper.getBalanceSheet({ table, id })`
- `paymentHelper.combine({ ids }, user)`
- `paymentHelper.getGateways(query?)`
- `paymentHelper.getPaymentsForInvoice(invoiceId, user)`
- `paymentHelper.savePaymentMethod(id, body, user)`
- `paymentHelper.importPaymentMethod(data, user)`

### Example

```js
// Charge a customer using a payment method
await paymentHelper.chargeCC({ payment_method_id: 12, invoice: 5, amount: 100 }, currentUser);

// Retrieve available payment gateways
const gateways = await paymentHelper.getGateways({ active: true });

// Get the balance sheet for a customer or invoice
const balanceSheet = await paymentHelper.getBalanceSheet({ table: 'customers', id: 12 });

// Save or update a payment method
await paymentHelper.savePaymentMethod(10, { card_number: '**** **** **** 1234' }, currentUser);

// Import a payment method from a gateway
await paymentHelper.importPaymentMethod({ gateway_id: 2, customer: 12 }, currentUser);

// Combine multiple payment transactions into a group
await paymentHelper.combine({ ids: [1,2,3] }, currentUser);

// Retrieve payments applied to an invoice
const payments = await paymentHelper.getPaymentsForInvoice(5, currentUser);
```

---

## SMS Helper (`smsHelper`)

Handles SMS-related operations, including sending, receiving, syncing, and managing conversations through different SMS gateways.

### Common Methods

* `smsHelper.sendSMS({ gateway_id, text, to, from, ...data }, user)`
* `smsHelper.getGateway(gateway_id)`
* `smsHelper.setupReceiveSMS(gateway_id, data)`
* `smsHelper.receiveSMS(gateway_id, data)`
* `smsHelper.refreshGateway(gateway_id)`
* `smsHelper.syncConversationsFromGateway(gateway_id)`
* `smsHelper.getConversations({ gateway_id, ...query }, user)`

### Example

```js
// Send an SMS through a specific gateway
await smsHelper.sendSMS({
  gateway_id: 1,
  text: 'Hello from Support!',
  to: '15551234567',
  from: '15559876543',
  table_name: 'customers',
  table_id: 12
}, currentUser);

// Set up webhook for receiving SMS
await smsHelper.setupReceiveSMS(2, { url: 'https://example.com/sms-webhook' });

// Handle incoming SMS from a gateway
await smsHelper.receiveSMS(2, { from: '15551234567', to: '15559876543', text: 'Hi there!' });

// Refresh gateway connection or configuration
await smsHelper.refreshGateway(3);

// Sync SMS conversations from gateway
await smsHelper.syncConversationsFromGateway(1);

// Retrieve all SMS conversations for a specific gateway
const conversations = await smsHelper.getConversations({ gateway_id: 1 }, currentUser);
```

---

## Templates Helper (`templatesHelper`)

Generates dynamic text content by replacing placeholders within template strings using data from one or more models. Supports batch (mail-merge style) output.

### Common Methods

* `templatesHelper.buildTemplate(str, models, user)`
* `templatesHelper.buildTemplates(arr, models, user, batch_mode?, email_field?)`

### Description

| Method           | Purpose                                                                                                                            |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `buildTemplate`  | Replace variables inside a single string template using data from the provided models.                                             |
| `buildTemplates` | Replace variables inside multiple templates. Supports **batch mode** to create recipient-based variations (e.g., email campaigns). |

### Models Format

Each model should be in the form:

```js
{ name: "table_name", id: 12 }
```

or with a pre-loaded record:

```js
{ name: "table_name", record: { ...data } }
```

### Example Usage

```js
// Single template replacement
const output = await templatesHelper.buildTemplate(
  "Hello ${customer.first_name}, your order #${order.id} is confirmed!",
  [
    { name: "customer", id: 42 },
    { name: "order", id: 91 }
  ],
  currentUser
);

// Multiple templates
const outputList = await templatesHelper.buildTemplates(
  [
    "Dear ${customer.first_name}",
    "Your balance is ${customer.balance}"
  ],
  [{ name: "customer", id: 42 }],
  currentUser
);

// Batch mode (mailing list style)
const batch = await templatesHelper.buildTemplates(
  ["Hello ${customer.first_name}, we have an update for you!"],
  [{ name: "customer", id: [10, 11, 12] }],
  currentUser,
  true, // batch_mode
  "email" // field used for recipient address
);

// Result will contain:
// batch.text  -> template rewritten with %recipient.field% placeholders
// batch.data  -> array of recipient records (email + fields used)
```
---


Use these modules responsibly and ensure proper error handling in your scripts. Only interact with exposed methods as documented above.

