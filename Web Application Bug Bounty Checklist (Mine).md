
A practical checklist for authorized testing of web applications and APIs. Use only assets and techniques permitted by the program. Follow program rules for automation, test accounts, data access, rate limits, and proof of impact. Stop if testing risks service availability or exposes real user data. Prefer test accounts, harmless markers, and minimal proof.

## Program and target setup

**Program / scope URL:**  
**In-scope host(s):**  
**Out-of-scope assets / techniques:**  
**Testing date and account(s):**  
**Rate limits / automation rules:**  
**Notes and evidence location:**  

- [ ] Read and record the program's scope, exclusions, safe harbor, and reporting rules.
- [ ] Confirm the exact hostname, application, API, and account roles in scope.
- [ ] Create only permitted test accounts and use synthetic data.
- [ ] Record a normal baseline request and response before changing inputs.
- [ ] Keep requests low volume; do not perform denial-of-service, broad password attacks, destructive actions, or tests against other users.
- [ ] For each finding, record affected endpoint, account role, minimal reproduction, impact, and redacted evidence.

---

## SQL injection

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Target / endpoint / parameter:**  
**Evidence / notes:**  

- [ ] Identify inputs that may reach database queries: query parameters, search, filters, forms, headers, and API fields.
- [ ] Compare normal input with harmless syntax variations; look for consistent database errors or changes in response behavior.
- [ ] Use only non-destructive, time-bounded checks allowed by the program; avoid extracting records or modifying data.
- [ ] Confirm suspected behavior with a minimal proof on your own test data and document the exact request/response difference.

## Authentication

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Flow / account role:**  
**Evidence / notes:**  

- [ ] Check registration, login, logout, MFA, recovery, and reauthentication flows with test accounts.
- [ ] Compare responses for valid and invalid test usernames to identify account enumeration.
- [ ] Check throttling and lockout behavior with a few controlled attempts, respecting program limits.
- [ ] Verify password reset tokens expire, are single-use, and are bound to the intended test account.
- [ ] Check OAuth/OIDC state, redirect URI validation, and account-linking behavior where offered.
- [ ] Confirm authentication changes invalidate sessions as expected; do not test against other users' accounts.

## Path traversal

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Feature / parameter:**  
**Evidence / notes:**  

- [ ] Identify file or path inputs, such as download names, image paths, exports, or document previews.
- [ ] Use harmless traversal probes to check whether path normalization or allowlisting fails.
- [ ] Confirm only with an approved, non-sensitive file or a controlled canary; do not read system files or secrets.
- [ ] Record whether access crosses the intended application directory boundary and the least-impact proof.

## Command injection

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Feature / parameter:**  
**Evidence / notes:**  

- [ ] Look for inputs passed to server-side utilities, such as diagnostics, file conversion, or import tools.
- [ ] Use only benign, non-mutating indicators permitted by the program; do not run commands that alter files, access secrets, or affect service health.
- [ ] Compare behavior with a baseline and confirm that any observed effect is caused by server-side command interpretation.
- [ ] Report the input, context, and minimal harmless evidence; do not establish persistence or retrieve data.

## Business logic vulnerabilities

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Workflow / feature:**  
**Evidence / notes:**  

- [ ] Map a workflow from start to finish using your own test account and records.
- [ ] Try permitted step reordering, repetition, cancellation, and incomplete submissions.
- [ ] Check whether prices, quantities, discounts, state, or ownership are trusted from client input; use sandbox or test transactions only.
- [ ] Verify that one-time actions and benefits cannot be reused beyond intended rules.
- [ ] Explain the violated business rule and demonstrate impact only with synthetic data.

## Information disclosure

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Location / data type:**  
**Evidence / notes:**  

- [ ] Review responses, errors, public files, source maps, metadata, and client-side bundles for unintended sensitive information.
- [ ] Check whether unauthenticated pages or your own account expose data beyond their intended audience.
- [ ] Do not collect, download, or include real personal data or secrets in proof; redact evidence and report location and type.
- [ ] Distinguish harmless version details from information that creates a concrete security impact.

## Access control

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Roles / object type:**  
**Evidence / notes:**  

- [ ] Create two or more test accounts with different roles or tenants if allowed.
- [ ] Compare access to your own objects across roles and accounts by changing object identifiers in requests.
- [ ] Check function-level permissions by requesting privileged actions as a lower-privilege test account.
- [ ] Verify authorization is enforced server-side and not only by hidden UI elements or client-supplied fields.
- [ ] Use only records you created; stop if a request reveals another person's data.

## File upload vulnerabilities

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Upload feature / allowed types:**  
**Evidence / notes:**  

- [ ] Check extension, content-type, file signature, size, filename, and storage validation with harmless test files.
- [ ] Verify uploaded content is stored and served with safe permissions and content handling.
- [ ] Check access control, overwrite behavior, and whether files are isolated between test accounts.
- [ ] Do not upload malware, exploit files, or content intended to execute on the server; avoid oversized files.

## Race conditions

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Action / workflow:**  
**Evidence / notes:**  

- [ ] Identify a state-changing action that should occur once, such as redeeming a test coupon or submitting a sandbox transaction.
- [ ] Use only a small, bounded number of near-simultaneous requests against your own test records.
- [ ] Check for duplicated effects, inconsistent balances, or invalid state transitions.
- [ ] Stop immediately if the test affects real payments, inventory, users, or service stability; document the minimal reproducible result.

## Server-side request forgery (SSRF)

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Feature / parameter:**  
**Evidence / notes:**  

- [ ] Identify server-side URL fetchers such as import-by-URL, webhook validation, previews, or image fetching.
- [ ] Use a domain or callback endpoint you control and is permitted by the program to confirm a server-side request.
- [ ] Do not target cloud metadata, internal networks, localhost, or third-party systems unless the program explicitly authorizes that exact testing.
- [ ] Record the callback evidence and demonstrate impact without retrieving internal content.

## XXE injection

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**XML endpoint / content type:**  
**Evidence / notes:**  

- [ ] Identify endpoints that accept XML or convert document formats that may process XML.
- [ ] Use a safe, non-exfiltrating canary technique approved by the program to check external entity processing.
- [ ] Do not attempt to read local files, access internal services, or cause resource exhaustion.
- [ ] Capture only the minimum response or controlled callback evidence needed to confirm behavior.

## NoSQL injection

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Endpoint / field:**  
**Evidence / notes:**  

- [ ] Identify JSON or form fields used in login, search, filtering, or record lookup.
- [ ] Check whether the server accepts unexpected types or query operators where a scalar value is expected.
- [ ] Use test accounts and harmless conditions; avoid bypassing access to real accounts or extracting records.
- [ ] Compare baseline and modified responses and record the smallest proof of server-side query manipulation.

## API testing

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**API / version / role:**  
**Evidence / notes:**  

- [ ] Inventory documented and observed endpoints, methods, parameters, and authentication requirements.
- [ ] Check object- and function-level authorization with your own accounts and records.
- [ ] Review input validation, mass assignment, pagination limits, error handling, and sensitive response fields.
- [ ] Check rate limits with a small number of requests and respect program guidance.
- [ ] For GraphQL, review schema exposure and resolver authorization under the dedicated GraphQL section below.
- [ ] Do not enumerate or download other users' data to establish impact.

## Web cache deception

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Page / cache layer:**  
**Evidence / notes:**  

- [ ] Identify personalized pages that may be cached by a CDN or reverse proxy.
- [ ] Using only your own account, request a page with a harmless path or extension variation and inspect cache headers and response behavior.
- [ ] Check whether a cacheable response can be served across your own separate test sessions.
- [ ] Do not attempt to retrieve another user's cached content; report the cache behavior and potential exposure with redacted evidence.

## Cross-site scripting (XSS)

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Input / output location:**  
**Evidence / notes:**  

- [ ] Trace user-controlled input into HTML, attributes, scripts, URLs, and DOM sinks.
- [ ] Use a harmless proof-of-concept that runs only in your test account or a program-provided environment.
- [ ] Check reflected, stored, and DOM-based contexts; verify output encoding and sanitization.
- [ ] Avoid payloads that steal cookies, access other users' sessions, or affect users outside the program's safe testing process.
- [ ] Record the affected context, execution conditions, and minimal screenshot or response evidence.

## Cross-site request forgery (CSRF)

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Action / endpoint:**  
**Evidence / notes:**  

- [ ] Identify state-changing actions performed with ambient browser credentials.
- [ ] Review CSRF tokens, SameSite cookie settings, origin checks, and content-type enforcement.
- [ ] Demonstrate only against your own test account and a harmless reversible action.
- [ ] Confirm whether a cross-site request can change state without valid user intent; do not target other users.

## Cross-origin resource sharing (CORS)

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Endpoint / origin behavior:**  
**Evidence / notes:**  

- [ ] Check CORS responses for trusted, untrusted, and null origins using requests to in-scope endpoints.
- [ ] Review `Access-Control-Allow-Origin`, credentials, methods, and headers together.
- [ ] Determine whether sensitive authenticated responses are readable cross-origin using your own test account.
- [ ] Report only if the behavior exposes meaningful data or actions; avoid accessing other users' information.

## Clickjacking

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Page / action:**  
**Evidence / notes:**  

- [ ] Review frame protections such as CSP `frame-ancestors` and `X-Frame-Options`.
- [ ] Test whether a relevant in-scope page can be framed in a local proof page.
- [ ] Assess only meaningful actions using a test account and non-destructive workflow.
- [ ] Record the affected page, missing protection, and realistic user impact.

## DOM-based vulnerabilities

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Page / source / sink:**  
**Evidence / notes:**  

- [ ] Identify client-side sources such as URL parameters, fragments, messages, and storage.
- [ ] Trace data to DOM or script-sensitive sinks and determine whether it is safely encoded.
- [ ] Validate with a harmless proof in your own session and record the source-to-sink path.
- [ ] Check related DOM behaviors such as unsafe redirects or HTML injection without affecting other users.

## WebSockets

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Endpoint / message type:**  
**Evidence / notes:**  

- [ ] Identify WebSocket endpoints, handshake authentication, origin checks, and message formats.
- [ ] Check authorization for subscriptions, rooms, and actions using your own test accounts.
- [ ] Review input validation and whether session changes or logout revoke the connection.
- [ ] Send only bounded, harmless test messages; do not subscribe to or inspect other users' channels.

## Insecure deserialization

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Endpoint / format:**  
**Evidence / notes:**  

- [ ] Identify serialized client-controlled data in cookies, tokens, request bodies, or imported files.
- [ ] Check for unsafe trust of serialized values using non-executing, harmless test variations.
- [ ] Do not use payloads that execute commands, write files, or cause service disruption.
- [ ] Document the format, integrity protections, and minimal evidence of unsafe processing.

## Web LLM attacks

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Feature / data boundary:**  
**Evidence / notes:**  

- [ ] Identify in-scope LLM features, connected tools, and the data each feature is intended to access.
- [ ] Use benign prompt-injection tests with synthetic content to check whether untrusted input overrides intended instructions.
- [ ] Check whether the feature reveals data across users or triggers actions beyond the test account's authorization.
- [ ] Do not submit real secrets, attempt to access other users' data, or invoke external actions without explicit program permission.
- [ ] Record the prompt, context, observed response, and concrete security impact.

## GraphQL API vulnerabilities

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Endpoint / operation:**  
**Evidence / notes:**  

- [ ] Identify the GraphQL endpoint, authentication model, and available operations from permitted sources.
- [ ] Check resolver authorization for objects and actions using your own test accounts.
- [ ] Review input validation, field-level access, error disclosure, and bounded query complexity controls.
- [ ] Avoid high-depth or high-volume queries that could degrade service; do not retrieve other users' data.

## Server-side template injection (SSTI)

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Template feature / field:**  
**Evidence / notes:**  

- [ ] Identify user-controlled values rendered into server-side templates, such as previews, emails, or reports.
- [ ] Use harmless arithmetic or template markers to distinguish literal rendering from server-side evaluation.
- [ ] Do not attempt command execution, file reads, or environment-variable disclosure.
- [ ] Record the rendering context and minimal non-invasive evidence.

## Web cache poisoning

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Endpoint / cache key behavior:**  
**Evidence / notes:**  

- [ ] Identify cacheable responses and headers or inputs that may influence the response but not the cache key.
- [ ] Test only with a unique harmless marker and a cache-busting or isolated test path where possible.
- [ ] Verify the response using your own session and avoid poisoning shared content used by other users.
- [ ] Stop after confirming behavior; report cache key mismatch and a safe reproduction.

## HTTP Host header attacks

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Endpoint / affected flow:**  
**Evidence / notes:**  

- [ ] Review whether host-related headers influence redirects, absolute links, password-reset emails, or cache behavior.
- [ ] Use only a controlled domain or test mailbox to check whether untrusted host values are reflected or trusted.
- [ ] Do not send crafted links to real users or attempt credential/token capture.
- [ ] Record the affected flow and minimal evidence of security impact.

## HTTP request smuggling

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Host / proxy path:**  
**Evidence / notes:**  

- [ ] Test only when the program explicitly permits request-smuggling checks and the target path is safe for them.
- [ ] Prefer a program-provided environment or controlled test endpoint; coordinate with the program where required.
- [ ] Use low-volume, non-destructive differential checks and stop if responses become unstable or affect other requests.
- [ ] Do not attempt to access other users' requests or poison shared traffic; report only minimal timing/response evidence.

## OAuth authentication

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Provider / callback:**  
**Evidence / notes:**  

- [ ] Review redirect URI validation, state and nonce use, PKCE where applicable, and callback handling.
- [ ] Check account linking and identity matching with test accounts you control.
- [ ] Verify authorization codes and tokens are bound to the correct client, redirect, and session.
- [ ] Do not target third-party accounts or attempt to capture another user's authorization code.

## JWT attacks

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Token location / service:**  
**Evidence / notes:**  

- [ ] Identify JWT use and inspect claims, expiry, audience, issuer, and key identifiers without sharing live tokens.
- [ ] Check whether the server validates the expected algorithm, signature, and relevant claims.
- [ ] Use only your own test token and non-privileged claims; do not forge access to other accounts or roles.
- [ ] Redact tokens in all evidence and report the validation flaw with a minimal test-account proof.

## Prototype pollution

**Status:** [ ] Not tested  [ ] Tested  [ ] Finding  
**Input / component:**  
**Evidence / notes:**  

- [ ] Identify nested JSON or object-merge inputs processed by client or server code.
- [ ] Use harmless properties and test accounts to see whether inherited properties affect application behavior.
- [ ] Avoid changing authorization, executing code, or impacting shared application state.
- [ ] Record the affected component, observable behavior, and a minimal safe proof.

---

## Finding write-up and closeout

**Finding title:**  
**Affected asset and endpoint:**  
**Severity / rationale:**  
**Test account / role:**  
**Steps to reproduce:**  
**Observed result:**  
**Expected result:**  
**Impact:**  
**Redacted evidence:**  
**Suggested remediation:**  

- [ ] Reproduce with the fewest requests and least impact possible.
- [ ] Remove secrets, session tokens, and personal data from evidence.
- [ ] Include clear impact and realistic attack prerequisites; label unconfirmed leads as such.
- [ ] Check program rules before submitting and avoid duplicate reports.
- [ ] Clean up test artifacts and retest only within the program's rules.
