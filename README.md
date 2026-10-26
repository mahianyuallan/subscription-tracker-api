# Subscription Tracker API

A REST API for tracking recurring subscriptions and emailing renewal reminders, built with Node.js, Express and MongoDB.

Built while following JavaScript Mastery's subscription tracker course; this repository is my implementation of it.

## What is implemented

- **JWT authentication:** sign-up and sign-in with bcrypt-hashed passwords; an `authorize` middleware protects routes.
- **Subscriptions:** create a subscription and list a user's subscriptions. The Mongoose model validates price, currency, frequency and category and computes the next renewal date.
- **Renewal reminders:** creating a subscription starts an Upstash Workflow that sleeps until 7, 5, 2 and 1 days before renewal and sends a reminder email through Nodemailer each time.
- **Rate limiting and bot protection** on every route with Arcjet.
- **Central error handling** for Mongoose validation, duplicate-key and cast errors.

Not finished: sign-out is an empty handler, and these routes return a fixed placeholder message: update, delete and cancel subscription, upcoming renewals, and user create, update and delete.

## Endpoints

All routes are under `/api/v1`.

| Method and path | Status |
|---|---|
| `POST /auth/sign-up`, `POST /auth/sign-in` | Implemented |
| `GET /users`, `GET /users/:id` (auth) | Implemented |
| `POST /subscriptions` (auth) | Implemented |
| `GET /subscriptions/user/:id` (auth) | Implemented |
| `POST /workflows/subscription/reminder` | Implemented (called by Upstash) |
| Other subscription and user routes | Placeholder |

## Tech stack

Node.js, Express, MongoDB with Mongoose, JSON Web Tokens, bcrypt, Arcjet, Upstash Workflow (QStash), Nodemailer.

## Quick start

**Prerequisites**

Make sure you have the following installed on your machine:

- [Git](https://git-scm.com/)
- [Node.js](https://nodejs.org/en)
- [npm](https://www.npmjs.com/) (Node Package Manager)

**Cloning the Repository**

```bash
git clone https://github.com/mahianyuallan/subscription-tracker-api.git
cd subscription-tracker-api
```

**Installation**

Install the project dependencies using npm:

```bash
npm install
```

**Set Up Environment Variables**

Create a new file named `.env.local` in the root of your project and add the following content:

```env
# PORT
PORT=5500
SERVER_URL="http://localhost:5500"

# ENVIRONMENT
NODE_ENV=development

# DATABASE
DB_URI=

# JWT AUTH
JWT_SECRET=
JWT_EXPIRES_IN="1d"

# ARCJET
ARCJET_KEY=
ARCJET_ENV="development"

# UPSTASH
QSTASH_URL=http://127.0.0.1:8080
QSTASH_TOKEN=

# NODEMAILER
EMAIL_PASSWORD=
```

**Running the Project**

```bash
npm run dev
```

Open [http://localhost:5500](http://localhost:5500) in your browser or any HTTP client to test the project.

## Sample subscription payload

<details>
<summary><code>Dummy JSON Data</code></summary>

```json
{
  "name": "Subaru Car payment",
  "price": 139.00,
  "currency": "USD",
  "frequency": "monthly",
  "category": "Loan repayment",
  "startDate": "2025-01-20T00:00:00.000Z",
  "paymentMethod": "Credit Card"
}
```

</details>

## Author

Built by [Allan Mwenja Mahianyu](https://www.allanmwenja.com/). More of my work is on [GitHub](https://github.com/mahianyuallan).
