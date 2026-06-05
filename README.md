# 🧪 API Testing — FakeStore API

A professional API testing project built with **Postman** and **Newman**, covering real-world scenarios including full CRUD operations, authentication, token handling, API chaining, JSON schema validation, and CI/CD integration via GitHub Actions.

---

## 📁 Project Structure

```
api-testing-demo/
├── .github/
│   └── workflows/
│       └── api-tests.yml        # GitHub Actions CI/CD
├── collections/
│   └── FakeStore API Testing.postman_collection.json
├── environments/
│   └── FakeStore - Dev.postman_environment.json
├── reports/
│   └── report.html              # Newman HTML Report
└── README.md
```

---

## ✅ Test Coverage

| # | Request | Method | Assertions |
|---|---------|--------|------------|
| 1 | Get All Products | GET | Status 200, Response time, Body not empty |
| 2 | Get Single Product | GET | Status 200, ID matches, Has title, Has price, Response time, JSON Schema |
| 3 | Add Product | POST | Status 201, Product ID exists, Title matches, Response time |
| 4 | Update Product | PUT | Status 200, Title updated, Price updated, Response time |
| 5 | Delete Product | DELETE | Status 200, Deleted ID matches, Response time |
| 6 | Login | POST | Status 201, Token exists |
| 7 | User Cart (Protected) | GET | Status 200, Response not empty |

**Total: 7 Requests — 24 Assertions — 0 Failed**

---

## 🛠️ Tech Stack

- [Postman](https://www.postman.com/) — API testing & collection management
- [Newman](https://github.com/postmanlabs/newman) — CLI test runner
- [newman-reporter-htmlextra](https://github.com/DannyDainton/newman-reporter-htmlextra) — HTML report generation
- [GitHub Actions](https://github.com/features/actions) — CI/CD automation
- [FakeStore API](https://fakestoreapi.com/) — Demo REST API

---

## 🚀 Getting Started

### Prerequisites

- Node.js (v20 or higher)
- Newman installed globally

```bash
npm install -g newman newman-reporter-htmlextra
```

---

### Run Tests (CLI)

```bash
newman run "collections/FakeStore API Testing.postman_collection.json" \
  -e "environments/FakeStore - Dev.postman_environment.json" \
  -r cli
```

---

### Generate HTML Report

```bash
newman run "collections/FakeStore API Testing.postman_collection.json" \
  -e "environments/FakeStore - Dev.postman_environment.json" \
  -r cli,htmlextra \
  --reporter-htmlextra-export reports/report.html
```

Then open `reports/report.html` in your browser.

---

## 🔐 Authentication & API Chaining

This project demonstrates **API Chaining** with token-based authentication:

1. **POST /auth/login** — Sends credentials, receives JWT token
2. Token is **automatically saved** to environment variable `{{authToken}}`
3. **GET /carts/user/2** — Uses `{{authToken}}` as Bearer token in Authorization header

No manual token copy-paste needed — fully automated.

---

## 📐 JSON Schema Validation

The `GET Single Product` request validates the full response structure:

```json
{
  "type": "object",
  "required": ["id", "title", "price", "category", "image"],
  "properties": {
    "id":          { "type": "number" },
    "title":       { "type": "string" },
    "price":       { "type": "number" },
    "description": { "type": "string" },
    "category":    { "type": "string" },
    "image":       { "type": "string" }
  }
}
```

---

## 🌍 Environment Variables

| Variable | Description |
|----------|-------------|
| `baseUrl` | Base URL of the API (`https://fakestoreapi.com`) |
| `authToken` | JWT token — auto-set after Login request |

---

## ⚙️ CI/CD — GitHub Actions

Tests run automatically on every `push` or `pull_request` to `main` branch.

**Workflow steps:**
1. Checkout code
2. Setup Node.js v20
3. Install Newman
4. Run API test collection
5. Upload HTML report as artifact

---

## 📊 Newman Output

```
FakeStore API Testing

→ GET All Products        200 OK       ✓ 3/3
→ GET Single Product      200 OK       ✓ 6/6
→ Add Product             201 Created  ✓ 4/4
→ Update Product          200 OK       ✓ 4/4
→ Delete Product          200 OK       ✓ 3/3
→ Login                   201 Created  ✓ 2/2
→ User Cart (Protected)   200 OK       ✓ 2/2

Requests: 7    Assertions: 24    Failed: 0
Total run duration: 2s
```

---

## 👨‍💻 Author

**Sumit Das**
