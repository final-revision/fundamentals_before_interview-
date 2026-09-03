# JWT, Security & Bcrypt Interview Questions & Answers

> Basic → Intermediate → Advanced + Practical/Project-based interview preparation for MERN / Node.js / Full-Stack interviews.

---

# PART 1 — Authentication & Authorization Basics

## 1. What is authentication?

**Answer:**

Authentication is the process of **verifying who a user is**.

```text
Email + Password
       ↓
Server verifies credentials
       ↓
User authenticated
```

---

## 2. What is authorization?

**Answer:**

Authorization determines **what an authenticated user is allowed to do**.

```text
Authentication → Who are you?
Authorization  → What are you allowed to do?
```

For example, an admin may be allowed to delete users, while a normal user cannot.

---

## 3. Authentication vs Authorization?

| Authentication | Authorization |
|---|---|
| Verifies identity | Verifies permissions |
| Happens first | Happens after authentication |
| "Who are you?" | "What can you access?" |
| Login | Role/permission checking |

### Example

```text
Login
 ↓
Authentication
 ↓
JWT generated
 ↓
Authorization
 ↓
Check user role
 ↓
Allow / Deny operation
```

---

# PART 2 — JWT Basics

## 4. What is JWT?

**Answer:**

JWT stands for **JSON Web Token**. It is a compact, URL-safe token format commonly used to transmit claims between a client and server.

It is commonly used for **authentication and authorization** in web applications.

---

## 5. Why is JWT used?

**Answer:**

JWT can be used to:

- Authenticate users
- Protect API routes
- Carry user claims
- Implement stateless authentication
- Implement role-based authorization

### Example Flow

```text
Login
 ↓
Server verifies user
 ↓
JWT generated
 ↓
Client receives JWT
 ↓
Client sends JWT with protected requests
 ↓
Server verifies JWT
```

---

## 6. What does a JWT look like?

A JWT has three parts:

```text
HEADER.PAYLOAD.SIGNATURE
```

Example:

```text
xxxxx.yyyyy.zzzzz
```

---

## 7. What are the three parts of JWT?

### 1. Header

Contains information about the token, such as the signing algorithm.

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### 2. Payload

Contains claims.

```json
{
  "userId": "123",
  "role": "admin"
}
```

### 3. Signature

Used to verify that the token has not been modified and, depending on the signing setup, that it was signed by a trusted issuer.

```text
Header + Payload + Secret/Private Key
                  ↓
               Signature
```

---

## 8. Is JWT encrypted?

**Answer:**

**No, a normal signed JWT is not encrypted.**

The payload is Base64URL-encoded, not encrypted.

Therefore, you should **never put sensitive information such as passwords, OTPs, or secret keys inside the JWT payload**.

---

## 9. Is JWT secure?

**Answer:**

JWT can be secure when implemented correctly.

Security depends on things such as:

- Strong signing keys
- Appropriate algorithms
- Short-lived access tokens
- Secure token storage
- HTTPS
- Proper signature verification
- Token expiration
- Correct authorization checks

JWT itself does not automatically make an application secure.

---

# PART 3 — JWT Authentication Flow

## 10. Explain JWT authentication flow.

```text
              LOGIN
                ↓
       Email + Password
                ↓
        Server verifies
          credentials
                ↓
        Generate JWT
                ↓
       Send token to client
                ↓
       Client stores token
                ↓
   Client requests protected API
                ↓
 Authorization: Bearer <token>
                ↓
       Server verifies JWT
                ↓
       User authenticated
                ↓
          API response
```

---

## 11. How do you create a JWT in Node.js?

Using the `jsonwebtoken` package:

```javascript
const jwt = require("jsonwebtoken");

const token = jwt.sign(
  { userId: user._id },
  process.env.JWT_SECRET,
  { expiresIn: "1h" }
);
```

---

## 12. How do you verify a JWT?

```javascript
const decoded = jwt.verify(
  token,
  process.env.JWT_SECRET
);

console.log(decoded);
```

If the token is invalid or expired, verification throws an error.

---

## 13. What is JWT_SECRET?

**Answer:**

`JWT_SECRET` is a secret value used to sign and verify JWTs when using a symmetric signing algorithm such as HS256.

It should **not be hardcoded in source code**.

Instead:

```env
JWT_SECRET=your-long-random-secret
```

And:

```javascript
process.env.JWT_SECRET
```

---

## 14. Why should JWT_SECRET be stored in `.env`?

**Answer:**

Because secrets should not be exposed in source code or committed to GitHub.

Instead of:

```javascript
jwt.sign(data, "mySecret123");
```

use:

```javascript
jwt.sign(data, process.env.JWT_SECRET);
```

---

# PART 4 — Access Token & Refresh Token

## 15. What is an access token?

**Answer:**

An access token is a short-lived credential used to access protected APIs.

```http
Authorization: Bearer <access-token>
```

---

## 16. What is a refresh token?

**Answer:**

A refresh token is a longer-lived credential used to obtain a new access token after the current access token expires.

### Typical Flow

```text
Login
 ↓
Access Token + Refresh Token
 ↓
Access token expires
 ↓
Refresh token sent to refresh endpoint
 ↓
New access token generated
```

---

## 17. Why use access tokens and refresh tokens?

**Answer:**

It provides a balance between:

- Security
- User experience
- Short-lived access credentials

The access token can have a short lifetime, reducing the impact if it is stolen.

---

## 18. Access token vs refresh token?

| Access Token | Refresh Token |
|---|---|
| Short-lived | Longer-lived |
| Used to access APIs | Used to obtain new access tokens |
| Sent frequently | Sent less frequently |
| More exposed | Should be protected carefully |

---

# PART 5 — JWT Storage

## 19. Where should JWT be stored?

**Answer:**

There isn't one universal answer; it depends on the application's threat model.

For browser-based applications, a common secure approach is to keep sensitive tokens in **Secure, HttpOnly cookies**, with appropriate `SameSite` settings and CSRF protection where needed.

Avoid casually storing long-lived authentication tokens in `localStorage`, because JavaScript-accessible storage can be exposed by an XSS vulnerability.

---

## 20. Why is localStorage considered risky for JWT?

**Answer:**

JavaScript can access `localStorage`.

If an attacker successfully executes malicious JavaScript through an XSS vulnerability, they may be able to read a token stored there.

```javascript
localStorage.getItem("token");
```

Therefore, storing sensitive authentication tokens in JavaScript-accessible storage requires careful consideration.

---

## 21. What is an HttpOnly cookie?

**Answer:**

An `HttpOnly` cookie cannot be read by JavaScript in the browser.

```javascript
res.cookie("refreshToken", token, {
  httpOnly: true,
  secure: true,
  sameSite: "strict"
});
```

This can reduce the risk of token theft through JavaScript-based XSS.

---

## 22. Does HttpOnly completely prevent XSS?

**Answer:**

No.

HttpOnly prevents JavaScript from directly reading the cookie, but it does **not** eliminate XSS itself.

XSS can still perform actions through the victim's browser, so applications still need proper input/output handling and other security controls.

---

# PART 6 — Bcrypt

## 23. What is bcrypt?

**Answer:**

bcrypt is a password-hashing algorithm designed specifically for securely hashing passwords.

It is intentionally computationally expensive, which makes large-scale password guessing more difficult.

---

## 24. Why shouldn't passwords be stored directly?

Bad:

```text
password → database
```

If the database is compromised, attackers immediately obtain the passwords.

Instead:

```text
password
   ↓
bcrypt
   ↓
password hash
   ↓
database
```

---

## 25. What is password hashing?

**Answer:**

Hashing converts a password into a one-way derived value.

```text
"mypassword"
      ↓
   bcrypt
      ↓
"$2b$..."
```

You don't normally decrypt a password hash. During login, you verify whether the entered password matches the stored hash.

---

## 26. Is bcrypt encryption?

**Answer:**

**No.**

bcrypt is a **password-hashing function**, not encryption.

```text
Encryption
↓
Can be decrypted with a key

Hashing
↓
Designed to be one-way
```

---

## 27. What is a salt in bcrypt?

**Answer:**

A salt is random data incorporated into password hashing.

It ensures that the same password does not always produce the same hash.

```text
Password: hello123

Hash 1 → different
Hash 2 → different
```

even though the password is the same.

---

## 28. Why is salt important?

Without a unique salt, two users with the same password could have the same hash.

That can make precomputed attacks such as rainbow-table attacks more effective.

bcrypt handles salt generation as part of its normal operation.

---

## 29. What is bcrypt salt rounds / cost factor?

**Answer:**

The cost factor controls how computationally expensive bcrypt hashing is.

```javascript
bcrypt.hash(password, 10);
```

Here `10` is the cost factor.

A higher cost generally means more computation and therefore slower hashing.

The value should be chosen based on current hardware and application performance requirements rather than blindly copying a number.

---

# PART 7 — Bcrypt in Node.js

## 30. How do you hash a password using bcrypt?

```javascript
const bcrypt = require("bcrypt");

const hashedPassword = await bcrypt.hash(password, 10);
```

Then store:

```javascript
user.password = hashedPassword;
```

---

## 31. How do you compare a password with a bcrypt hash?

```javascript
const isMatch = await bcrypt.compare(
  password,
  user.password
);
```

If the password matches:

```javascript
true
```

Otherwise:

```javascript
false
```

---

## 32. Why don't we decrypt the bcrypt hash?

**Answer:**

Because bcrypt is a password-hashing function, not encryption.

Instead of decrypting:

```text
Password → Hash
```

you compare:

```text
Entered Password
       ↓
bcrypt.compare()
       ↓
Stored Hash
```

---

# PART 8 — Login System

## 33. Explain a secure login flow.

```text
User enters email + password
              ↓
        Find user
              ↓
      Get password hash
              ↓
    bcrypt.compare()
              ↓
       Password valid?
         ↙       ↘
       No         Yes
       ↓           ↓
   Reject       Generate
                  token
                    ↓
              Send authenticated
              response
```

---

## 34. What happens during registration?

```text
User submits password
        ↓
Validate input
        ↓
Hash password with bcrypt
        ↓
Store hash in database
        ↓
Never store plaintext password
```

---

## 35. What happens during login?

```text
User submits email + password
        ↓
Find user
        ↓
Compare password using bcrypt
        ↓
If valid
        ↓
Create authentication credential
        ↓
Return authenticated response
```

---

# PART 9 — Middleware & Protected Routes

## 36. What is authentication middleware?

**Answer:**

Authentication middleware checks whether a request contains valid authentication credentials before allowing it to reach a protected route.

```javascript
app.get(
  "/api/profile",
  authMiddleware,
  getProfile
);
```

---

## 37. How does JWT middleware work?

```text
Request
   ↓
Read Authorization header
   ↓
Extract Bearer token
   ↓
Verify JWT
   ↓
Get user information
   ↓
Attach user to req
   ↓
next()
```

### Example

```javascript
const authMiddleware = (req, res, next) => {
  const authHeader = req.headers.authorization;

  if (!authHeader?.startsWith("Bearer ")) {
    return res.status(401).json({
      message: "Authentication required"
    });
  }

  const token = authHeader.split(" ")[1];

  try {
    const decoded = jwt.verify(
      token,
      process.env.JWT_SECRET
    );

    req.user = decoded;
    next();
  } catch (error) {
    return res.status(401).json({
      message: "Invalid or expired token"
    });
  }
};
```

---

# PART 10 — Authorization & Roles

## 38. What is role-based access control?

**Answer:**

Role-Based Access Control, or RBAC, gives users permissions based on their roles.

```text
Admin
 ├── Create user
 ├── Delete user
 ├── Update user

User
 ├── View profile
 └── Update own profile
```

---

## 39. How can JWT be used for authorization?

JWT can contain claims such as:

```json
{
  "userId": "123",
  "role": "admin"
}
```

After verifying the token, the server can check the role before allowing an operation.

**Important:** authorization must be enforced by the server, not trusted merely because the client UI says the user is an admin.

---

# PART 11 — Common Security Questions

## 40. What is HTTPS?

**Answer:**

HTTPS is HTTP over TLS.

It encrypts data transmitted between the client and server and helps protect against network interception and tampering.

Authentication credentials and tokens should generally be transmitted over HTTPS.

---

## 41. What is XSS?

**Answer:**

XSS stands for **Cross-Site Scripting**.

It occurs when an attacker causes malicious JavaScript to execute in another user's browser.

### Potential Impact

- Stealing data accessible to JavaScript
- Performing actions as the victim
- Modifying page content
- Stealing non-HttpOnly tokens

---

## 42. What is CSRF?

**Answer:**

CSRF stands for **Cross-Site Request Forgery**.

It occurs when an attacker tricks a user's browser into sending an unwanted authenticated request to a website.

It is especially relevant when authentication credentials are automatically sent by the browser, such as cookies.

### Common Defenses

- SameSite cookies
- CSRF tokens
- Origin/Referer validation where appropriate

---

## 43. XSS vs CSRF?

| XSS | CSRF |
|---|---|
| Injects/executes malicious script | Tricks browser into making a request |
| Targets browser-side execution | Exploits automatically sent credentials |
| Input/output handling is important | CSRF defenses are important |
| HttpOnly cookies can reduce token theft | SameSite/CSRF tokens can help |

---

## 44. What is SQL injection?

**Answer:**

SQL injection occurs when attacker-controlled input is improperly included in SQL queries.

### Unsafe Example

```javascript
const query =
  "SELECT * FROM users WHERE email = '" + email + "'";
```

Use parameterized queries or a safe ORM/query builder instead.

---

## 45. What is NoSQL injection?

**Answer:**

NoSQL injection occurs when untrusted input is interpreted as a database query structure rather than ordinary data.

Applications using MongoDB should validate and sanitize request data and avoid blindly passing user-controlled objects into database queries.

---

## 46. Why should passwords be hashed and not encrypted?

**Answer:**

Passwords normally don't need to be recovered in their original form.

During login, we only need to verify whether the supplied password matches the stored password hash.

Therefore, a password hashing function such as bcrypt or Argon2 is appropriate.

---

# PART 12 — Token Expiration

## 47. What is token expiration?

**Answer:**

Token expiration limits how long an authentication token remains valid.

```javascript
jwt.sign(
  { userId: user._id },
  process.env.JWT_SECRET,
  { expiresIn: "15m" }
);
```

After the expiration time, the token should no longer be accepted.

---

## 48. Why should JWTs expire?

**Answer:**

If a token is stolen, a short expiration time limits the period during which it can be used.

For longer sessions, applications can use a refresh-token mechanism with appropriate protection and rotation/revocation strategies.

---

## 49. What happens when a JWT expires?

**Answer:**

The server's JWT verification fails because the token is expired.

The client can then:

- Ask the user to log in again, or
- Use a valid refresh-token flow to obtain a new access token.

---

# PART 13 — Common JWT Attacks / Mistakes

## 50. What happens if someone modifies the JWT payload?

**Answer:**

If the token's signature is properly verified, modifying the payload will cause signature verification to fail.

Example:

```text
Original:
role = user

Attacker changes:
role = admin
```

The modified token won't have a valid signature.

---

## 51. Can users change their JWT role from user to admin?

**Answer:**

They can technically modify the encoded payload, but they **cannot create a valid signature** without the required signing secret/private key.

The server must always verify the token before trusting its claims.

---

## 52. What happens if JWT_SECRET is leaked?

**Answer:**

If a symmetric JWT signing secret is compromised, an attacker may be able to create valid-looking tokens.

The application should:

- Rotate the secret
- Invalidate/revoke affected tokens where possible
- Investigate the compromise
- Force reauthentication if necessary
- Ensure the secret is removed from exposed locations

---

## 53. Should you put passwords in JWT?

**Answer:**

**Never.**

JWT payloads are readable by whoever possesses the token.

Never put:

```text
password
credit card number
secret key
OTP
```

inside a normal JWT payload.

---

# PART 14 — Cookies vs Authorization Header

## 54. How can JWT be sent to the server?

Two common approaches are:

### Authorization Header

```http
Authorization: Bearer <token>
```

### Cookie

```http
Cookie: accessToken=<token>
```

Cookies can be configured with security attributes such as:

```text
HttpOnly
Secure
SameSite
```

---

## 55. Which is better: cookies or localStorage?

**Interview Answer:**

> It depends on the application's architecture and threat model. For browser applications, HttpOnly Secure cookies are often preferred for sensitive authentication credentials because JavaScript cannot directly read HttpOnly cookies. If cookies are used for authentication, CSRF protections and appropriate SameSite settings should also be considered.

Avoid saying:

> "localStorage is always insecure."

The better answer is that **JavaScript-accessible storage increases the impact of XSS if an attacker can execute JavaScript**.

---

# PART 15 — API Security

## 56. How do you secure a REST API?

Important practices include:

```text
HTTPS
 ↓
Authentication
 ↓
Authorization
 ↓
Input Validation
 ↓
Password Hashing
 ↓
Rate Limiting
 ↓
Secure Headers
 ↓
CORS Configuration
 ↓
Error Handling
 ↓
Logging & Monitoring
```

---

## 57. What is rate limiting?

**Answer:**

Rate limiting restricts how many requests a client can make within a specific period.

Example:

```text
100 requests / minute / IP
```

It can help protect against:

- Brute-force attacks
- Credential stuffing
- API abuse
- Excessive resource consumption

---

## 58. What is brute-force attack?

**Answer:**

A brute-force attack repeatedly tries possible passwords or credentials until one works.

### Defenses

- Rate limiting
- Account lockout or progressive delays where appropriate
- Strong passwords
- MFA
- Monitoring

---

## 59. What is input validation?

**Answer:**

Input validation ensures that data received from users follows expected rules before it is processed.

Example:

```text
email must be valid
password must meet requirements
age must be a number
```

Validation should happen on the **server**, even if the frontend also validates the data.

---

## 60. Why should we not trust frontend validation?

**Answer:**

Because users can bypass frontend code.

For example, a user can directly send:

```http
POST /api/users
```

without using your React application.

Therefore:

```text
Frontend validation → Better UX
Backend validation  → Security / correctness
```

---

# PART 16 — Practical MERN Interview Questions

## 61. Explain JWT authentication in your MERN project.

### Interview-Ready Answer

> In my MERN project, I implemented authentication using JWT. During registration, I validate the user's input and hash the password using bcrypt before storing it in MongoDB. During login, I retrieve the user and compare the entered password with the stored bcrypt hash. If the credentials are valid, the backend issues an authentication token. Protected routes use middleware to verify the token before allowing access. I also use authorization checks for role-specific operations and return appropriate HTTP status codes.

---

## 62. Explain registration flow.

```text
React
 ↓
POST /api/auth/register
 ↓
Express Route
 ↓
Validation
 ↓
Check existing user
 ↓
bcrypt.hash()
 ↓
MongoDB
 ↓
Response
```

---

## 63. Explain login flow.

```text
React
 ↓
POST /api/auth/login
 ↓
Find User
 ↓
bcrypt.compare()
 ↓
Valid?
 ↓
Generate Token
 ↓
Send Authentication Response
```

---

## 64. Explain a protected route.

```text
Client
 ↓
GET /api/profile
 ↓
Authentication Middleware
 ↓
Extract Credentials
 ↓
Verify JWT
 ↓
Authorization Check if required
 ↓
Controller
 ↓
Database
 ↓
Response
```

---

# PART 17 — Tricky Interview Questions

## 65. Can JWT be revoked?

**Answer:**

A self-contained JWT is typically valid until it expires unless the application has a mechanism to reject it.

For stronger revocation control, applications can use mechanisms such as:

- Short-lived access tokens
- Refresh-token rotation
- Server-side token/session records
- Token deny lists for specific use cases

---

## 66. What if a JWT is stolen?

**Answer:**

An attacker may be able to use the stolen token until it expires or is otherwise invalidated.

Therefore:

- Use HTTPS
- Keep access tokens short-lived
- Protect token storage
- Use secure cookies where appropriate
- Implement refresh-token rotation/revocation where appropriate
- Monitor suspicious activity

---

## 67. Is JWT better than sessions?

**Answer:**

Neither is universally better.

### JWT

Useful when you want:

- Stateless access-token validation
- Distributed services
- APIs used by multiple clients

### Sessions

Useful when you want:

- Server-side control over sessions
- Easy revocation
- Traditional web application authentication

The correct choice depends on the application's architecture and requirements.

---

## 68. JWT vs Session Authentication?

| JWT | Session |
|---|---|
| Token contains claims | Server stores session state |
| Can be stateless | Stateful |
| Easy to pass between services | Requires session storage |
| Revocation needs additional design | Session can be invalidated server-side |
| Useful for APIs | Common in traditional web applications |

---

## 69. What is the difference between hashing, encryption and encoding?

### Hashing

```text
Password → Hash
```

Designed to be one-way.

Examples:

```text
bcrypt
Argon2
```

### Encryption

```text
Data → Encrypted Data → Decrypted Data
```

Reversible with the correct key.

### Encoding

```text
Data → Encoded Data → Decoded Data
```

Designed for representation/transmission, not security.

Example:

```text
Base64
```

---

# ⭐ TOP 25 QUESTIONS TO DEFINITELY PREPARE

If you're a **fresher preparing for a MERN/full-stack placement**, prioritize these:

```text
1. What is authentication?
2. What is authorization?
3. Authentication vs authorization?
4. What is JWT?
5. Why is JWT used?
6. What are the three parts of JWT?
7. Is JWT encrypted?
8. How does JWT authentication work?
9. What is JWT_SECRET?
10. Why use environment variables for secrets?
11. What is bcrypt?
12. Why hash passwords?
13. Hashing vs encryption?
14. What is salt?
15. What are bcrypt salt rounds?
16. How do you hash a password with bcrypt?
17. How do you compare a password with bcrypt?
18. What is authentication middleware?
19. How do protected routes work?
20. What is role-based authorization?
21. What is XSS?
22. What is CSRF?
23. How do you secure a REST API?
24. Access token vs refresh token?
25. Explain JWT authentication in your MERN project.
```

---

# 🔥 The Most Important Flow to Memorize

```text
                REGISTER
                   │
                   ▼
          Email + Password
                   │
                   ▼
            Input Validation
                   │
                   ▼
             bcrypt.hash()
                   │
                   ▼
               MongoDB
                   │
                   ▼
                 LOGIN
                   │
                   ▼
          Email + Password
                   │
                   ▼
            Find User
                   │
                   ▼
          bcrypt.compare()
                   │
             ┌─────┴─────┐
             │           │
          Invalid       Valid
             │           │
             ▼           ▼
           401       Generate Token
                         │
                         ▼
                 Client Authentication
                         │
                         ▼
                 Protected API Request
                         │
                         ▼
                Auth Middleware
                         │
                         ▼
                   Verify Token
                         │
                         ▼
               Authorization Check
                         │
                         ▼
                    Controller
                         │
                         ▼
                     MongoDB
                         │
                         ▼
                    API Response
```

---

# 🎯 Final Interview Revision

Before your interview, make sure you can explain these without memorizing a definition:

```text
Authentication
Authorization
JWT
JWT Header
JWT Payload
JWT Signature
JWT_SECRET
Access Token
Refresh Token
Token Expiration
HttpOnly Cookie
bcrypt
Password Hashing
Salt
Salt Rounds / Cost Factor
bcrypt.hash()
bcrypt.compare()
Authentication Middleware
Protected Routes
RBAC
HTTPS
XSS
CSRF
SQL Injection
NoSQL Injection
Rate Limiting
Input Validation
JWT vs Sessions
Hashing vs Encryption vs Encoding
```

## One-Line Definitions

```text
Authentication → Verifies identity.

Authorization → Verifies permissions.

JWT → Token format commonly used for authentication/claims.

bcrypt → Password hashing algorithm.

Hashing → One-way transformation used for password verification.

Salt → Random value incorporated into password hashing.

Access Token → Short-lived credential used to access protected APIs.

Refresh Token → Credential used to obtain a new access token.

Middleware → Function that runs during request processing.

RBAC → Authorization based on user roles.

HTTPS → HTTP protected with TLS.

XSS → Attacker-controlled script execution in a user's browser.

CSRF → Tricks a browser into making an unwanted authenticated request.

Rate Limiting → Restricts request frequency.

CORS → Browser mechanism controlling cross-origin requests.
```
