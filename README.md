<h1 align="center">🛍️ Shop</h1>

<p align="center">
  A full-stack e-commerce application with a React frontend, Node.js/Express REST API, MongoDB, Stripe payments, and Cloudinary image hosting.
</p>

<p align="center">
  <a href="https://shop-lovat-seven.vercel.app">Live Demo</a> ·
  <a href="#api-overview">API Overview</a> ·
  <a href="#setup">Setup</a>
</p>

---

## Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [Features](#features)
- [Project Structure](#project-structure)
- [Setup](#setup)
- [Environment Variables](#environment-variables)
- [API Overview](#api-overview)
- [Security](#security)
- [Deployment](#deployment)
- [Screenshots](#screenshots)
- [Demo Credentials](#demo-credentials)
- [What This Project Demonstrates](#what-this-project-demonstrates)
- [Author](#author)

---

## Overview

**Shop** is a full-featured online store built with a client-server architecture. The React frontend communicates with a Node.js/Express backend over a REST API. The system supports customer-facing functionality (browsing, cart, checkout via Stripe, reviews) as well as a full admin panel (product/order/user management, sales statistics, deals).

> **Live Demo:** [https://shop-lovat-seven.vercel.app](https://shop-lovat-seven.vercel.app)
> **API Base URL:** *(add deployed backend URL here)*

---

## Tech Stack

### Frontend

| Technology | Purpose |
|---|---|
| React 18 | UI library |
| Redux Toolkit | Global state management |
| React Router v6 | Client-side routing |
| Tailwind CSS | Utility-first styling |
| Vite | Build tool and dev server |
| Axios | HTTP client |
| Chart.js + react-chartjs-2 | Data visualisation |
| @stripe/react-stripe-js | Stripe Checkout integration |
| AOS | Scroll-triggered animations |
| Toastr | Toast notifications |
| Remix Icons | Icon set |

### Backend

| Technology | Purpose |
|---|---|
| Node.js | Runtime environment |
| Express 5 | Web framework |
| Mongoose | MongoDB ODM |
| JSON Web Tokens (JWT) | Stateless authentication |
| bcrypt | Password hashing |
| Cloudinary | Image upload and storage |
| Stripe | Payment processing |
| Helmet | Secure HTTP headers |
| express-rate-limit | Request rate limiting |
| express-mongo-sanitize | NoSQL injection protection |
| cors | Cross-origin resource sharing |
| cookie-parser | HTTP cookie handling |

---

## Features

### Customer

- Registration and login with JWT authentication
- Product browsing with search and filtering
- Persistent shopping cart (localStorage)
- Stripe Checkout — hosted payment page
- Post-payment order confirmation and history
- Product reviews (create, edit, delete)
- Profile management (username, avatar, bio)
- Personal purchase statistics

### Admin

- Dashboard with sales statistics and charts
- Full product CRUD (with Cloudinary image upload)
- Order management with status updates
- User management (view, role change, delete)
- Deals / special offers management

---

## Project Structure

```
Shop/
├── frontend/                 # React client (Vite)
│   ├── src/
│   │   ├── components/       # Shared UI components (Navbar, Footer, etc.)
│   │   ├── pages/
│   │   │   ├── home/         # Landing page
│   │   │   ├── shop/         # Product catalogue + checkout flow
│   │   │   └── dashboard/
│   │   │       ├── admin/    # Admin panel pages
│   │   │       └── user/     # User dashboard pages
│   │   ├── redux/
│   │   │   ├── features/     # Auth, cart, products, orders slices
│   │   │   └── store.js
│   │   ├── routers/          # Route definitions and guards
│   │   └── utils/            # Shared utilities (baseURL, etc.)
│   ├── public/
│   ├── .env.example          # Required environment variables
│   └── package.json
│
├── backend/                  # Node.js/Express API
│   ├── src/
│   │   ├── auth/             # Auth-check route (verifyToken guard)
│   │   ├── users/            # Registration, login, logout, profile
│   │   ├── products/         # Product CRUD
│   │   ├── orders/           # Orders, Stripe Checkout, payment confirm
│   │   ├── reviews/          # Product reviews
│   │   ├── deal/             # Deals / special offers
│   │   ├── stats/            # Aggregate sales statistics
│   │   ├── middleware/       # verifyToken, verifyAdmin, generateToken
│   │   └── utils/            # uploadImage (Cloudinary), globalLimiter
│   ├── index.js              # App entry point
│   ├── .env.example          # Required environment variables
│   └── package.json
│
├── er-diagram.puml           # Database ER diagram (PlantUML)
├── use-case.puml             # Use-case diagram (PlantUML)
└── README.md
```

---

## Setup

### Prerequisites

- Node.js 18+
- npm
- MongoDB instance (local or [MongoDB Atlas](https://www.mongodb.com/atlas))
- [Cloudinary](https://cloudinary.com/) account
- [Stripe](https://stripe.com/) account

### 1. Clone the repository

```bash
git clone <repository-url>
cd Shop-master
```

### 2. Install and start the backend

```bash
cd backend
npm install
cp .env.example .env   # fill in your values
npm start
```

Backend runs at `http://localhost:5000`.
The start script uses `nodemon`; install it globally with `npm i -g nodemon` if it is not already available.

### 3. Install and start the frontend

```bash
cd frontend
npm install
cp .env.example .env   # fill in your values
npm start
```

Frontend runs at `http://localhost:5173`.

---

## Environment Variables

### `backend/.env`

See [`backend/.env.example`](./backend/.env.example) for all keys and inline descriptions.

| Variable | Description |
|---|---|
| `PORT` | Port the Express server listens on (default `5000`) |
| `DATABASE` | MongoDB connection string |
| `JWT_SECRET` | Secret used to sign JWT tokens |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret |
| `STRIPE_SECRET_KEY` | Stripe secret key (server-side) |
| `API_BASE_URL` | Frontend base URL — used to build Stripe redirect URLs |

### `frontend/.env`

See [`frontend/.env.example`](./frontend/.env.example) for all keys and inline descriptions.

| Variable | Description |
|---|---|
| `VITE_API_BASE_URL` | Backend API base URL |
| `VITE_STRIPE_PK` | Stripe publishable key (client-side) |

---

## API Overview

All endpoints are prefixed with the backend base URL. Authentication is carried via an `HttpOnly` cookie set on login.

### Auth — `/api/auth`

| Method | Path | Auth | Description |
|---|---|---|---|
| `POST` | `/api/auth/register` | Public | Register a new user |
| `POST` | `/api/auth/login` | Public | Login; sets `token` cookie |
| `POST` | `/api/auth/logout` | Public | Clears auth cookie |
| `PATCH` | `/api/auth/edit-profile` | Public | Update username, avatar, bio |
| `GET` | `/api/auth/user` | Public | List all users |
| `PUT` | `/api/auth/user/:id` | Admin | Update user role |
| `DELETE` | `/api/auth/user/:id` | Admin | Delete user |

### Auth Check — `/auth-check`

| Method | Path | Auth | Description |
|---|---|---|---|
| `GET` | `/auth-check` | Token | Validate the active session |

### Products — `/api/product`

| Method | Path | Auth | Description |
|---|---|---|---|
| `GET` | `/api/product` | Public | List products (filterable) |
| `GET` | `/api/product/:id` | Public | Get product by ID |
| `POST` | `/api/product` | Admin | Create product |
| `PUT` | `/api/product/:id` | Admin | Update product |
| `DELETE` | `/api/product/:id` | Admin | Delete product |

### Orders — `/api/order`

| Method | Path | Auth | Description |
|---|---|---|---|
| `POST` | `/api/order/create-checkout-session` | Token | Create a Stripe Checkout session |
| `POST` | `/api/order/confirm-payment` | Token | Confirm payment and persist order |
| `GET` | `/api/order/:email` | Public | Get orders by customer email |
| `GET` | `/api/order/order/:id` | Public | Get order by ID |
| `GET` | `/api/order` | Public | Get all orders |
| `PATCH` | `/api/order/update-order-status/:id` | Admin | Update order status |
| `DELETE` | `/api/order/delete-order/:id` | Public | Delete order |

### Reviews — `/api/review`

| Method | Path | Auth | Description |
|---|---|---|---|
| `GET` | `/api/review/:productId` | Public | Get reviews for a product |
| `POST` | `/api/review` | Token | Post a review |
| `PUT` | `/api/review/:id` | Token | Edit a review |
| `DELETE` | `/api/review/:id` | Token | Delete a review |

### Deals — `/api/deal`

| Method | Path | Auth | Description |
|---|---|---|---|
| `GET` | `/api/deal` | Public | List deals |
| `POST` | `/api/deal` | Admin | Create deal |
| `PUT` | `/api/deal/:id` | Admin | Update deal |
| `DELETE` | `/api/deal/:id` | Admin | Delete deal |

### Stats — `/api/stats`

| Method | Path | Auth | Description |
|---|---|---|---|
| `GET` | `/api/stats` | Admin | Get sales statistics |

### Image Upload

| Method | Path | Auth | Description |
|---|---|---|---|
| `POST` | `/uploadImage` | Public | Upload image to Cloudinary |

---

## Security

- **Helmet** — sets secure HTTP response headers (XSS, clickjacking, MIME sniffing protection)
- **express-rate-limit** — global request rate limiting to mitigate brute-force and DDoS
- **express-mongo-sanitize** — strips `$` operators from request data to prevent NoSQL injection
- **bcrypt** — passwords are hashed with salt before storage; plain-text passwords are never persisted
- **JWT** — tokens are signed with a secret and delivered via `HttpOnly`, `Secure`, `SameSite=None` cookies
- **CORS** — restricted to known frontend origin(s)
- **xss-clean** — the dependency is present in `package.json`; the middleware is currently commented out in `index.js`

---

## Deployment

Both services are configured for [Vercel](https://vercel.com/) using the `vercel.json` files in each subdirectory.

### Deploy backend

```bash
cd backend
npx vercel --prod
```

Add the variables from `backend/.env.example` as environment variables in the Vercel project dashboard.

### Deploy frontend

```bash
cd frontend
npx vercel --prod
```

Add the variables from `frontend/.env.example` in the Vercel project dashboard.
Set `VITE_API_BASE_URL` to the deployed backend URL before building.

---

## Screenshots

> *Add screenshots once the live demo is available.*

| Page | Preview |
|---|---|
| Home | — |
| Product List | — |
| Product Detail | — |
| Cart & Checkout | — |
| Admin Dashboard | — |

---

## Demo Credentials

> *Add credentials if the live demo has a seeded test account.*

| Role | Email | Password |
|---|---|---|
| Admin | `admin@example.com` | — |
| Customer | `user@example.com` | — |

---

## What This Project Demonstrates

- **Full-stack architecture** — decoupled React SPA communicating with a REST API
- **JWT authentication** — token issuance, `HttpOnly` cookie transport, and middleware-protected routes
- **Role-based access control** — customer vs. admin middleware guards on API routes
- **Stripe Checkout** — hosted payment flow with post-payment session retrieval and order persistence
- **Cloudinary integration** — image upload and CDN delivery for product images
- **Redux Toolkit** — scalable state management across auth, cart, and product slices
- **Admin panel** — CRUD operations, order lifecycle management, and Chart.js visualisations
- **Security hardening** — Helmet headers, rate limiting, and NoSQL injection sanitisation
- **Vercel deployment** — separate frontend and backend projects with environment variable configuration

---

## Author

**Ihnat Tryhub**

---

*ISC License*
