# Trello API Testing with Postman

API testing project built as part of the **GoIT QA Manual** course (Block 2 — Flexible QA, Practice 4: Postman).

This repository contains a complete Postman collection for testing the **Trello REST API**, including JavaScript test assertions for status codes, response times, and data type validation.

---

## Project Overview

This project demonstrates end-to-end API testing of the Trello platform using Postman. The collection covers full CRUD operations on Trello boards, lists, and cards, with automated tests on each endpoint.

### What is tested

| # | Task | Method | Endpoint |
|---|------|--------|----------|
| 1 | Create a Board | `POST` | `/boards/` |
| 2 | Create a List (Left) | `POST` | `/lists` |
| 3 | Create a List (Right) | `POST` | `/lists` |
| 4 | Create a Card (in Left List) | `POST` | `/cards` |
| 5 | Create a Card (in Right List) | `POST` | `/cards` |
| 6 | Delete a Card | `DELETE` | `/cards/{id}` |
| 7 | Get All Cards on a Board | `GET` | `/boards/{id}/cards` |
| 8 | Update a Board | `PUT` | `/boards/{id}` |

### Test assertions used

- **Status code validation** — every request must return `200 OK`
- **Response time validation** — must complete in under `1500 ms`
- **Data type validation** — selected fields (`id`, `name`) must be of type `string`

### Automated variable chaining

The collection uses Postman environment variables to chain requests together. IDs returned from earlier requests (`boardId`, `leftListId`, `rightListId`, `leftCardId`) are automatically saved to the environment via test scripts and reused in later requests — no manual copy-paste required.

---

## Getting Started

### Prerequisites

- A free [Postman](https://www.postman.com/downloads/) account (desktop app or web version)
- A free [Trello](https://trello.com) account
- A Trello API Key and Token — generate at [trello.com/power-ups/admin](https://trello.com/power-ups/admin)

### Installation

1. Clone or download this repository.
2. Import both files into Postman:
   - `Trello_Homework_Collection.postman_collection.json` — the collection
   - `Trello_Homework_Environment.postman_environment.json` — the environment template
3. Open the **Trello HW Environment** in Postman and fill in your own values:
   - `apiKey` — your Trello API key
   - `apiToken` — your Trello API token
4. Select **Trello HW Environment** in the top-right dropdown.
5. Run the requests in order (Task 1 → Task 8). IDs will be saved automatically between requests.

---

## Sample Test Script

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 1500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1500);
});

pm.test("'id' is a string", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.id).to.be.a('string');
});

// Save the board ID to environment for subsequent requests
const jsonData = pm.response.json();
pm.environment.set("boardId", jsonData.id);
```

---

## Security Notes

- **API credentials are never committed to this repository.** The environment file contains only placeholders.
- Treat your Trello API key and token as you would a password — never share them publicly or commit them to a repo.
- If you accidentally expose a token, [revoke it](https://trello.com/power-ups/admin) immediately.

---

## Skills Demonstrated

- REST API testing with **Postman**
- Writing automated test scripts in **JavaScript** (Postman test sandbox)
- Working with **environment variables** and dynamic data chaining
- Handling multiple HTTP methods: `GET`, `POST`, `PUT`, `DELETE`
- Reading API documentation (Trello REST API v1)
- Status code, response time, and schema validation
- Building reusable, importable test collections

---

## Author

**Mariia Pshenychna**
QA Manual student, GoIT
Potsdam, Germany

---

## License

This project is available for educational and portfolio purposes. Feel free to fork and adapt for your own learning.
