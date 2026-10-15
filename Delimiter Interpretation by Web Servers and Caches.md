
## 1. `%00` (Null byte)

- **OpenLiteSpeed:**
  - Treats `%00` as a delimiter → truncates path at `%00`.
  - Example: `/profile%00.css` → interpreted as `/profile`.
- **Akamai / Fastly (CDNs):**
  - May treat `%00` as a literal → the cache key is `/profile%00.css`, not `/profile`.
- **Apache / NGINX / Node.js:**
  - Typically reject or sanitize `%00` → returns 400 or 404.

## 2. `%2F` (Encoded slash)

- **NGINX:**
  - Decodes `%2F` → becomes a real `/`. This can lead to path confusion.
  - `/api%2Fv1` becomes `/api/v1`.
- **Apache (with AllowEncodedSlashes off):**
  - Rejects or returns 404 on `%2F`.
- **Akamai / CloudFront:**
  - Often cache based on raw path → keeps `%2F` encoded. Can lead to origin vs cache mismatch.

## 3. `;` (Semicolon)

- **Apache / Tomcat:**
  - Treats `;` as the beginning of path parameters. `/index.php;a=b` → `/index.php`.
- **Fastly / Cloudflare:**
  - Include `;a=b` in the cache key → caches `/index.php;a=b`.
- **Spring Boot (Java):**
  - Parses `;` as matrix parameter delimiter, ignores it in routing by default.

## 4. `?` and `#` (Query and Fragment)

- **All HTTP servers:**
  - `?` starts query string → included in cache key by CDNs like Cloudflare, Akamai.
  - `#` is never sent to the server → irrelevant to server-side cache logic.

## 5. `%09`, `%20` (Tab and Space encoding)

- **Some caches (e.g., Akamai):**
  - Normalize or strip whitespace characters → `/path%20img.js` might normalize to `/path img.js`.
- **Origin servers:**
  - May reject or misinterpret these, depending on framework.

## 6. Double slashes `//`

- **NGINX / Apache:**
  - Normalize to a single slash unless configured otherwise.
- **CDNs (Cloudflare, etc.):**
  - Might treat `/foo//bar` as distinct from `/foo/bar` → cache miss.

## 7. Case Sensitivity

- **S3 / CloudFront / Akamai:**
  - Case-sensitive: `/Profile` ≠ `/profile`.
- **Windows IIS:**
  - Case-insensitive: `/Profile` == `/profile`.
- **Cache key mismatches:**
  - Can be abused to serve cached content to different endpoints.
