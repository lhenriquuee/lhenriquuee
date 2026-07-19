# Ticket Status API — Integration Guide

**Author:** Luís Henrique Miranda  
**Type:** API Reference Documentation (Sample Portfolio Project)  
**Audience:** Backend developers and integration partners  

---

## About this project

This documentation was created as a portfolio sample to demonstrate API reference writing for a support/helpdesk platform. It shows how to authenticate against the platform and how to programmatically update the status of a support ticket through a REST endpoint — a common integration pattern for CRM, ITSM, and customer support tools.

> [!NOTE]
> This is a fictionalized, English-language rewrite of a real internal API I documented professionally. Field names, sample payloads, and error codes have been adapted for a public portfolio and do not expose any proprietary system.

---

## Table of contents

- [Overview](#overview)
- [Authentication](#authentication)
- [Update ticket status](#update-ticket-status)
- [Status values reference](#status-values-reference)
- [Error handling](#error-handling)
- [Quick start example](#quick-start-example)

---

## Overview

The Ticket Status API lets an external system update the status of a support ticket directly on the platform — for example, when a ticket is resolved in a third-party tool and needs to be reflected back automatically, instead of relying on manual updates by an agent.

**Base URL**

```http
https://api.example-helpdesk.com
```

All requests and responses use `application/json`.

---

## Authentication

Before calling any other endpoint, your integration must obtain an access token.

### `POST /api/user/login`

| Parameter  | Type   | Required | Description                                                         |
| :--------- | :----- | :------- | :------------------------------------------------------------------ |
| `login`    | string | Yes      | Username of an account authorized to change ticket statuses         |
| `password` | string | Yes      | Password for the account above                                      |

**Request Example**

```json
POST /api/user/login
Content-Type: application/json

{
  "login": "api.user",
  "password": "your-password"
}
```

**Successful Response**

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

Include this token in the `Authorization` header of every subsequent request:

```http
Authorization: Bearer <accessToken>
```

**Possible Errors**

| Error message               | Cause                                                              |
| :-------------------------- | :----------------------------------------------------------------- |
| `User not found`            | The `login` value does not match any account                       |
| `Invalid password`          | Credentials do not match                                           |
| `login field is required`   | Request body is missing `login`                                    |
| `password field is required`| Request body is missing `password`                                 |
| `Access denied`             | Account lacks permission to authenticate for this API              |
| `Token is missing`          | No token was sent on a request that requires one                   |
| `Token expired`             | The access token's validity window has passed — request a new one  |
| `Invalid token signature`   | The token was altered or is not recognized by the server           |

### Required Permission

The account used for authentication must have the **"Update ticket status via API"** permission enabled in its user profile. Without it, authentication succeeds but status-update requests will be rejected.

---

## Update ticket status

### `POST /api/tickets/status`

Updates the status of an existing ticket, identified by its ticket number.

**Headers**

| Header           | Value                  |
| :--------------- | :--------------------- |
| `Authorization`  | `Bearer <accessToken>` |
| `Content-Type`   | `application/json`     |

**Body Parameters**

| Parameter  | Type   | Required                                                           | Description                                                                  |
| :--------- | :----- | :----------------------------------------------------------------- | :--------------------------------------------------------------------------- |
| `ticketId` | string | Yes                                                                | The ticket number to update                                                  |
| `status`   | string | Yes                                                                | New status. See [Status values reference](#status-values-reference)          |
| `reason`   | string | Only for `Cancelled`, `Rejected`, or reopening a `Closed` ticket   | A pre-registered reason justifying the status change                         |

**Request Example**

```json
POST /api/tickets/status
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json

{
  "ticketId": "20260709-0001",
  "status": "Closed",
  "reason": "Issue resolved and confirmed with the customer"
}
```

**Successful Response**

```json
{
  "message": "Ticket updated successfully"
}
```

---

## Status values reference

| Status              | Description                              | Requires `reason`? |
| :------------------ | :--------------------------------------- | :----------------- |
| `Open`              | Ticket created, not yet assigned         | No                 |
| `In progress`       | An agent is actively working on the ticket| No                 |
| `Cancelled`         | Ticket cancelled before resolution       | Yes                |
| `Rejected`          | Ticket deemed invalid or out of scope    | Yes                |
| `Closed`            | Ticket resolved and finished             | No                 |
| `Closed` → reopened | Reopening a previously closed ticket     | Yes                |

---

## Error handling

| Error message               | Cause                                                          |
| :-------------------------- | :------------------------------------------------------------- |
| `Ticket not found`          | The `ticketId` does not match any existing ticket              |
| `Status not found`          | The `status` value is not one of the accepted values           |
| `reason field is required`  | A `reason` was required for this status change but not sent    |

---

## Quick start example

```bash
# 1. Authenticate to get the token
curl -X POST https://api.example-helpdesk.com/api/user/login \
  -H "Content-Type: application/json" \
  -d '{"login": "api.user", "password": "your-password"}'

# 2. Update the ticket status using the token
curl -X POST https://api.example-helpdesk.com/api/tickets/status \
  -H "Authorization: Bearer <accessToken>" \
  -H "Content-Type: application/json" \
  -d '{"ticketId": "20260709-0001", "status": "Closed", "reason": "Issue resolved"}'
```

---

## About the writer

Luís Henrique is a Technical Writer with a deep background in IT infrastructure and systems support, specializing in Docs-as-Code workflows using Markdown, Git, and GitHub. He writes product documentation, API references, user guides, and release notes for B2B software platforms.

- **GitHub:** [github.com/lhenriquuee](https://github.com/lhenriquuee)
- **LinkedIn:** [linkedin.com/in/luis-henrique-miranda](https://www.linkedin.com/in/luis-henrique-miranda/)
