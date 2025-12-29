## **Advanced URL Policy Matching (Dynamic URLs & User Variables)**

The Policies System supports **dynamic URL matching**, allowing URL access rules to be defined using **user-based variables**, **path parameters**, and **query conditions**.

This enables fine-grained authorization such as:

* Allowing users to access **only their own resources**
* Restricting access based on **user identity or attributes**
* Matching dynamic URLs without hardcoding IDs

---

### **URL Exception Evaluation Rules**

* URL exceptions are evaluated **after** basic policy checks.
* The actual request URL is matched against the policy exception **pattern**.
* Policy patterns may include:

  * Static paths
  * Path variables
  * Query parameters
  * User-based variable substitutions
* Only the parameters defined in the policy are enforced. Extra URL parameters are ignored.

---

### **1. Path Parameter Matching**

URL path segments may contain **user variables**.

**Format:**
`url:/path/:user.{field}`

**Example:**
`url:/customer/:user.id`

**Behavior:**

* `/customer/123` → Allowed if `user.id === 123`
* `/customer/124` → Denied

**Nested Paths:**

* `url:/customer/:user.id/orders`
* Matches: `/customer/123/orders`
* Does **not** match: `/customer/123/profile`

---

### **2. Query Parameter Matching**

Query parameters may also reference user variables.

**Format:**
`url:/path?param=:user.{field}`

**Example:**
`url:/someuser?id=:user.id`

**Behavior:**

* `/someuser?id=123` → Allowed if `user.id === 123`
* `/someuser?id=999` → Denied
* `/someuser?id=123&extra=x` → Allowed (extra params ignored)

---

### **3. Supported Operators**

By default, user variables use **exact match**.
Optional operators can be applied for advanced matching.

**Syntax:**
`:user.{field}~{operator}`

| Operator       | Description                               |
| -------------- | ----------------------------------------- |
| `eq` (default) | Exact match                               |
| `startsWith`   | URL value must start with the user value  |
| `includes`     | URL value must contain the user value     |
| `regex`        | URL value must match a regular expression |

---

### **Operator Examples**

**Starts With**

```
url:/customer/:user.id~startsWith
```

* `/customer/12345` → Allowed if `user.id = 123`

**Includes**

```
url:/search?q=:user.email~includes
```

**Regex (Query or Path)**

```
url:/orders?id=:user.id~regex(^\d\d*$)
```

⚠️ **Important:**
When using regex in query parameters, special characters such as `+` **must be URL-encoded** (e.g. `%2B`) to ensure correct parsing.

---

### **4. Combined Path + Query Rules**

Path and query rules can be combined.

**Example:**

```
url:/customer/:user.id?tab=orders
```

**Behavior:**

* `/customer/123?tab=orders` → Allowed
* `/customer/123?tab=profile` → Denied

---

### **5. URL Parsing Behavior**

* URL patterns are split on the **first** `?`
* Additional `?` characters are treated as part of the query string
* URL-encoded values are decoded before comparison
* Malformed or unsupported patterns safely fail and deny access

---

### **Best Practices**

* Prefer **exact matching** (`eq`) for identity-based authorization
* Use `startsWith` / `includes` only for non-security-critical matching
* Avoid complex regex when simpler operators suffice
* Keep policy exceptions explicit and minimal for auditability

