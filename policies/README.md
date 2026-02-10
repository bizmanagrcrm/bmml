# Policies System Documentation

## Overview

The Policies System controls user access within our platform. Each user is assigned a **policy**, which defines what they are allowed to access. Policies are stored in the database and are enforced throughout the system.

## Navigating to the Policies Manager

To create or edit policies (some actions require **root** permission), navigate to:

📍 **`{YOUR_BZMNG_BASE_URL}/admin#/permission-policies`**

## Assigning a Policy to a User

To attach a policy to a user:

1. Go to **`{YOUR_BZMNG_BASE_URL}/admin#/employees`**.
2. Right-click on the user you want to modify.
3. Select **"Change Policy"**.
4. Follow the steps to assign a new policy.

## Policy Structure

A policy consists of the following key attributes:

| Attribute    | Type     | Description |
|-------------|---------|-------------|
| `name`      | `text`  | Unique identifier for the policy. |
| `allow_all` | `bool`  | If `true`, the policy is a **blacklist** (default access is allowed, except for defined exceptions). If `false`, it is a **whitelist** (default access is denied, except for defined exceptions). |
| `exceptions` | `text[]` | A list of specific permissions that are either explicitly **allowed** or **denied**, based on `allow_all`. |
| `is_system` | `bool`  | If `true`, the policy is a system policy and cannot be deleted. |
| `default_for` | `text` | Specifies which user group this policy is assigned to by default. |

## Exception Types

The `exceptions` array defines specific rules within the policy. Each exception follows a structured format:

### **1. CRUD Operations**
Grants or restricts access to specific CRUD actions on database tables.

**Format:**  
`crud:{table}:{action}:{filter_clm=filter_val}`

**Example:**  
- `crud:orders:read:customer_id=42` → Allows reading only orders where `customer_id=42`.
- `crud:users:update:role=admin` → Allows updating only users with role "admin".

### **2. URL Access**
Grants or restricts access to specific URLs.

**Format:**  
`url:/{url_to_whitelist}`

**Example:**  
- `url:/admin/reports` → Grants access to the `/admin/reports` page.
- `url:/api/v1/products` → Grants API access to the `/api/v1/products` endpoint.


## Session Variables in Policy Exceptions

Policy exceptions support **dynamic session variables** that are resolved at runtime from the current session user. This allows policies to be scoped per user without hardcoding values.

### Syntax

Session variables use double brackets and a `user.` path:

- `[[user.id]]`
- `[[user.email]]`
- `[[user.role]]`
- `[[user.<field>]]`

At request time, these placeholders are replaced with the corresponding value from the session’s user object.

### Supported Locations

Session variables can be used in **exception filters** (the `{filter_clm=filter_val}` part of a CRUD exception).

**CRUD format:**  
`crud:{table}:{action}:{filter_clm=filter_val}`

### Example

Restrict users to reading only their own records:

```

crud:contacts:read:owner=[[user.id]]

```

At runtime, this is evaluated as if it were:

```

crud:contacts:read:owner=<current_user_id>

```

### Typical Configuration

To enforce “users can only access their own resources”:

- `allow_all = false` (whitelist mode)
- `exceptions = ['crud:contacts:read:owner=[[user.id]]']`

**Result:**
- Internal users only see records they own.
- API users only see records they own.
- No cross-user data leakage occurs.

### Behavior Notes

- Session variables are resolved **per request**.
- If a referenced user field does not exist or is `null`, the exception will not match any records.
- This feature is intended for access scoping (e.g. per-user, per-tenant).

## Default Policies

There are **four default system policies**, each automatically assigned to the appropriate user type:

| Policy Name                   | `allow_all` | `is_system` | Assigned To  |
|--------------------------------|------------|------------|--------------|
| **Default Internal User Policy** | `true`     | `true`     | `internal`   |
| **Default API Policy**          | `true`     | `true`     | `api`        |
| **Default Customer Policy**      | `false`    | `true`     | `customer`   |
| **Default Public Policy**        | `false`    | `true`     | `public`     |

## Summary

- Policies control user access.
- **`allow_all = true`** → Blacklist mode (default allow, except exceptions).
- **`allow_all = false`** → Whitelist mode (default deny, except exceptions).
- Exceptions can be **CRUD-based** (table operations) or **URL-based** (specific pages or API endpoints).
- Default policies are preconfigured and assigned to different user types.

---
🚀 **For any modifications or to create custom policies, visit:**  
📍 **`{YOUR_BZMNG_BASE_URL}/admin#/permission-policies`**

