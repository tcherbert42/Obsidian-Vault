# Lab 1: API Security — VulnMart Submission Report

**Course**: CSC4585 Software & Systems Security  
**Student**: Thomas Herbert  
**Date**: October 2, 2026  

---

## 1. Final Required Comparison Table

| TODO | Security Control | Vulnerable Result | Secure Result | Status Code(s) Observed |
|---|---|---|---|---|
| **1** | **JWT secret management** | Hardcoded predictable secret (`"vulnmart-secret-123"`) in source code allows token forgery by anyone who inspects the file. | Secret loaded from `VULNMART_JWT_SECRET` environment variable with secure fallback (`secrets.token_hex(32)`) if unset. | Configuration / Implementation inspection |
| **2** | **Restrictive CORS** | Permissive wildcard CORS (`origins: "*"`) reflected arbitrary untrusted origins (`http://evil.example`) along with `Access-Control-Allow-Credentials: true`. | CORS restricted to explicit allowlist (`http://127.0.0.1:5001`, `http://localhost:5001`); untrusted origin receives no allow header; credentials removed. | `200 OK` (Vulnerable reflected header; Secure omitted allow header) |
| **3** | **JWT expiration** | Token had no `iat` or `exp` claims and remained valid indefinitely. | Token includes `iat` and `exp` claims (3-minute lifetime). Expired tokens are rejected with unauthorized error. | Initial: `200 OK`<br>Expired: `401 Unauthorized` |
| **4** | **Rate limiting** | Throttling was not called; 1000 consecutive requests succeeded without restriction. | Rate limiter active on `/api/login` and `/api/register`. Requests beyond 5 within a 60s window are blocked. | Vulnerable: `200 OK` (1000/1000)<br>Secure: `200 OK` (4), `429 Too Many Requests` (996) |
| **5** | **Registration mass assignment & input validation** | Client supplied `balance: 999999` and `is_admin: 1`; server stored values directly into database. Malformed inputs were rejected by basic length checks. | Server assigns safe defaults (`balance = 0.0`, `is_admin = 0`) ignoring client parameters. Malformed input returns validation error. | Valid/Mass-assigned: `201 Created`<br>Malformed: `400 Bad Request` |
| **6** | **Profile BOLA / excessive data exposure** | Authenticated user (Alice) retrieved Bob's profile (`/api/users/2`). Query returned all columns including `ssn`, `password_hash`, `balance`, and `is_admin`. | Object-level authorization enforces ownership via `require_same_user`. Query limited strictly to `id`, `username`, `email`. Alice accessing Bob is blocked. | Alice on self: `200 OK`<br>Alice on Bob: `403 Forbidden` (Secure) vs `200 OK` (Vuln) |
| **7** | **Update ownership / property authorization** | Alice modified her own `balance` to 999999 and `is_admin` to 1, and updated Bob's account email without authorization. | Alice blocked from modifying Bob's account (`require_same_user`). Allowed fields restricted to `["email"]`; attempts to modify protected properties are rejected. | Modifying other: `403 Forbidden`<br>Protected field: `400 Bad Request`<br>Valid field: `200 OK` |
| **8** | **Orders BOLA** | Alice retrieved Bob's order collection (`/api/users/2/orders`) without ownership verification. | Enforced `require_same_user` check before querying orders. Bob's order collection blocked for Alice. | Alice on self: `200 OK`<br>Alice on Bob: `403 Forbidden` (Secure) vs `200 OK` (Vuln) |
| **9** | **Single-order BOLA** | Alice retrieved Bob's single order (`/api/orders/3`) by simply providing the order ID. | Query parameterized to filter by both `id = ?` and `user_id = ?`. Bob's order is not exposed to Alice. | Alice on self (`/1`): `200 OK`<br>Alice on Bob (`/3`): `404 Not Found` (Secure) vs `200 OK` (Vuln) |
| **10** | **Function-level authorization** | Non-admin user (Alice / Bob) accessed administrator endpoint (`/api/admin/users`) because endpoint only required `@require_auth`. | Changed decorator to `@require_admin`. Non-admin caller is rejected; only verified admins can access. | Non-admin: `403 Forbidden` (Secure) vs `200 OK` (Vuln)<br>Admin: `200 OK` |
| **11** | **SQL injection / XSS handling** | Raw search parameter concatenated into SQL string (`LIKE '%{search}%'`). Payload `' OR '1'='1` returned all users. Frontend rendered unescaped HTML. | Parameterized SQL treats input strictly as data (`LIKE ?`, `(%search%,)`). Search payload matches zero rows and returns `[]`. | `200 OK`<br>(Vuln: 5 rows dumped; Secure: `[]` empty array) |
| **12** | **API versioning / inventory** | `/api/health` returned generic `{"status":"ok"}` without version indication. | `/api/health` exposes `{"status":"ok","version":"v1"}`. API catalog documented in inventory. | `200 OK` |

---

## 2. Submission Questions & Answers

### 1. Why is authentication different from authorization?
**Authentication (AuthN)** verifies *identity*—answering the question, *"Who are you?"* (e.g., verifying a user's password or signature on a JWT).  
**Authorization (AuthZ)** verifies *permissions*—answering the question, *"Are you permitted to access this specific resource or perform this specific action?"* (e.g., verifying whether an authenticated user is the owner of an order or possesses administrator privileges). A request can be successfully authenticated while still being completely unauthorized.

---

### 2. Which TODOs implement object-level authorization?
- **TODO (6)** — Profile BOLA: Restricts `/api/users/<id>` so that a user can only retrieve their own profile (`require_same_user(user_id)`).
- **TODO (7)** — User Update Ownership: Restricts `PUT /api/users/<id>` so that a user cannot modify another user's account records.
- **TODO (8)** — Orders Collection BOLA: Restricts `/api/users/<id>/orders` so that a user cannot view another user's order history.
- **TODO (9)** — Single-Order Authorization: Restricts `/api/orders/<id>` by filtering the database query by both `id` and `current_user_id` so users cannot access orders belonging to other accounts.

---

### 3. Which TODOs prevent client-controlled sensitive properties?
- **TODO (5)** — Registration Mass Assignment: Hardcodes default values server-side (`balance = 0.0`, `is_admin = 0`) instead of accepting `balance` or `is_admin` from the client's JSON registration payload.
- **TODO (7)** — Property-Level Authorization on Update: Limits `allowed_fields` to `["email"]`, rejecting requests that attempt to modify protected properties such as `balance`, `is_admin`, or `ssn` with a `400 Bad Request`.

---

### 4. Why does parameterized SQL prevent the SQL injection checkpoint from changing query structure?
In raw string concatenation, user input is parsed as SQL command syntax by the SQL compiler, allowing metacharacters like `'`, `OR`, and `=` to alter the Abstract Syntax Tree (AST) of the query.  
With **parameterized queries (prepared statements)**, the database engine compiles the query structure *before* binding parameters. User input is transferred separately in a data channel and treated strictly as literal scalar values, meaning metacharacters cannot break out of data context to execute arbitrary SQL commands.

---

### 5. Why can preventing SQL injection alone be insufficient if a frontend renders untrusted API values using unsafe HTML insertion?
Preventing SQL injection ensures that data stored in or returned from the database is accurate and untampered with. However, if that data originates from untrusted sources (e.g., user-submitted profile names, comments, or external feeds) and the frontend inserts it into the DOM using unsafe APIs (such as `element.innerHTML`, `document.write()`, or unescaped string template literals), any embedded `<script>` tags or malicious event handlers (`<img onerror="...">`) will still execute in the victim's browser, leading to **Cross-Site Scripting (XSS)**. Security requires both secure data handling on the backend and context-aware encoding/safe DOM methods (`textContent`, `innerText`, DOM manipulation) on the frontend.

---

### 6. Why is returning a full database row dangerous even when access to the endpoint requires authentication?
Returning the complete database record (`SELECT *`) causes **Excessive Data Exposure** (OWASP API3:2023). Even if the client is authenticated, sensitive internal fields (such as `password_hash`, `ssn`, reset tokens, or internal flags) may be exposed in HTTP response bodies, network logs, browser caches, or client-side application state. If the endpoint also suffers from broken authorization (BOLA), an attacker can easily harvest sensitive PII and password hashes for all users. Endpoints should strictly employ data projection / Data Transfer Objects (DTOs) returning only the minimum necessary fields.

---

### 7. Why is an authenticated user not automatically authorized to access an administrator endpoint?
Authentication proves only that the caller holds valid user credentials; it provides no guarantee regarding the caller's role, permissions, or access tiers. In a role-based access control (RBAC) model, administrative endpoints perform sensitive privileged operations (e.g., listing all accounts, deleting resources, altering permissions). If an application only checks `@require_auth` without inspecting claims such as `is_admin == True`, any normal user can escalate their privileges to perform administrative actions (**Broken Function-Level Authorization / OWASP API5:2023**).

---

### 8. What behavior changed after rate limiting was implemented?
- **Vulnerable Application**: Allowed unlimited requests (tested up to 1,000 rapid POST requests to `/api/login`) with all requests returning `200 OK` in ~70 seconds, leaving the system vulnerable to brute-force credential stuffing, password guessing, and denial of service.
- **Secure Application**: Enforced a threshold of 5 attempts per IP within a 60-second window. The first 4 requests returned `200 OK`, and all subsequent attempts (requests 5 through 1,000) were blocked with `429 Too Many Requests`, completing in just 4.64 seconds without consuming database authentication overhead.

---

### 9. What is the purpose of token expiration?
Token expiration (via the `exp` claim in JWTs) limits the **window of vulnerability** if a token is compromised (e.g., intercepted via network snooping, leaked in client logs, stolen through XSS, or retained on an unattended machine). Without expiration, a stolen token grants permanent access until server keys are rotated. With expiration, an attacker's access window is strictly bounded, requiring the client to periodically re-authenticate or refresh their credentials.

---

### 10. What information should be maintained in an API inventory?
An effective API inventory (OWASP API9:2023 — Improper Inventory Management) should maintain:
1. **Endpoint Route / Path** (e.g., `/api/v1/users/<id>`)
2. **HTTP Methods** (GET, POST, PUT, DELETE, PATCH)
3. **API Version** (e.g., `v1`, `v2`, deprecated versions)
4. **Authentication Requirements** (Public, Bearer Token, API Key, mTLS)
5. **Authorization Policy / Roles** (Public, Owner Only, Admin Only, Scopes)
6. **Request Parameters & Schemas** (Headers, Query parameters, JSON payload schemas)
7. **Response Payloads & Status Codes** (Supported response formats, error codes)
8. **Environment / Host Deployment** (Development, Staging, Production URL / IP)
9. **Deprecation & Sunset Schedule** (Retirement dates for older API versions to avoid zombie/shadow APIs)

---

## 3. Verified API Inventory Table (Secure VulnMart v1)

| Endpoint | Method | Authentication | Authorization Policy | Description |
|---|---|---|---|---|
| `/api/login` | POST | No | Public (Rate limited: 5 req/min) | Issues JWT with `exp` and `iat` claims |
| `/api/register` | POST | No | Public (Rate limited: 5 req/min) | Registers user with default `balance=0`, `is_admin=0` |
| `/api/users/<id>` | GET | Yes (Bearer JWT) | Object Owner Policy (`require_same_user`) | Returns safe profile: `id`, `username`, `email` |
| `/api/users/<id>` | PUT | Yes (Bearer JWT) | Object Owner + Property Policy | Allows updating `email` only |
| `/api/users/<id>/orders` | GET | Yes (Bearer JWT) | Object Owner Policy (`require_same_user`) | Lists user's own orders collection |
| `/api/orders/<id>` | GET | Yes (Bearer JWT) | Order Owner Policy (`user_id = ?`) | Retrieves single order owned by user |
| `/api/admin/users` | GET | Yes (Bearer JWT) | Administrator Policy (`require_admin`) | Lists all users (Admin role required) |
| `/api/products` | GET | Yes (Bearer JWT) | Authenticated Search (Parameterized) | Safe user search by username |
| `/api/health` | GET | No | Public | Health and version status (`version: v1`) |
