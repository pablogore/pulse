# Pulse

**Pulse** is a protocol-agnostic client for **end-to-end testing** of backend systems, powered by a **DSL inspired by tools like Hurl**.

It lets you describe interactions and assertions against real services in a clean, expressive way, without coupling tests to HTTP, gRPC, or any specific transport.

Pulse tests systems as a **black box**, the way real clients do.

---

## ✨ Why Pulse?

Most E2E tests are tightly coupled to:

- HTTP clients
- gRPC stubs
- Framework-specific test utilities
- Internal service implementation

This makes tests fragile and not representative of real system behavior.

Pulse solves this with:

- A **protocol-agnostic execution engine**
- A **DSL for describing requests and expectations** (Hurl-style)
- Expressive assertions over real responses
- True black-box testing

---

## 🧠 Core Idea

Instead of writing Go code like:

```go
resp, _ := http.Post(...)
if resp.StatusCode != 200 { ... }
```

You write tests like this:

```go
POST /api/orders
Authorization: Bearer {{token}}
Content-Type: application/json

{
  "product_id": "123",
  "quantity": 2
}

HTTP 201
[Asserts]
jsonpath "$.orderId" exists
jsonpath "$.status" == "CREATED"
header "X-Correlation-Id" exists
