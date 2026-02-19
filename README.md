# 🛍️ LEBABA Shop

A modern e-commerce web application with full functionality for customers and administrators.

## 📋 Table of Contents

- [Project Description](#project-description)
- [Key Features](#key-features)
- [Technologies](#technologies)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [API Endpoints](#api-endpoints)
- [Functionality](#functionality)
- [Deployment](#deployment)
- [Author](#author)

## 📖 Project Description

**LEBABA Shop** is a full-featured online store built with a client-server architecture. The project includes a modern React frontend and a powerful Node.js backend with REST API. The system provides secure authentication, product management, orders, reviews, and statistics.

## ✨ Key Features

### For Customers:
- 🔐 Registration and authentication
- 🔍 Product search and filtering
- 🛒 Shopping cart
- 📦 Order placement and tracking
- ⭐ Product reviews
- 💳 Payment via Stripe
- 📊 Personal purchase statistics
- 👤 Profile management

### For Administrators:
- 🎛️ Dashboard
- 📦 Product management (CRUD operations)
- 📋 Order management
- 👥 User management
- 📈 Store statistics
- 🎁 Deals and special offers management
- 📊 Data visualization with charts

## 🛠️ Technologies

### Frontend:
- **React 18** — UI library
- **Redux Toolkit** — State management
- **React Router** — Routing
- **Tailwind CSS** — Styling
- **Vite** — Build tool and dev server
- **Axios** — HTTP client
- **Chart.js** — Statistics visualization
- **Stripe** — Payment integration
- **AOS** — Scroll animations
- **Toastr** — Notifications

### Backend:
- **Node.js** — Runtime environment
- **Express 5** — Web framework
- **Mongoose** — MongoDB ODM
- **JWT** — Authentication and authorization
- **bcrypt** — Password hashing
- **Cloudinary** — Image uploads
- **Stripe** — Payment processing
- **Helmet** — HTTP header security
- **express-rate-limit** — Request rate limiting
- **express-mongo-sanitize** — NoSQL injection protection
- **xss-clean** — XSS attack protection

## 📁 Project Structure

```
LEBABA Shop/
├── frontend/                 # Client-side
│   ├── src/
│   │   ├── components/       # Reusable components
│   │   │   ├── Navbar.jsx
│   │   │   ├── Footer.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   └── ...
│   │   ├── pages/           # Application pages
│   │   │   ├── home/        # Home page
│   │   │   ├── shop/        # Product store
│   │   │   ├── dashboard/   # Dashboard
│   │   │   │   ├── admin/   # Admin panel
│   │   │   │   └── user/    # User panel
│   │   │   └── ...
│   │   ├── redux/           # Redux store and slices
│   │   │   ├── features/
│   │   │   │   ├── auth/
│   │   │   │   ├── cart/
│   │   │   │   ├── products/
│   │   │   │   └── ...
│   │   │   └── store.js
│   │   ├── routers/         # Routing
│   │   └── utils/           # Utilities
│   ├── public/              # Static files
│   └── package.json
│
├── backend/                 # Server-side
│   ├── src/
│   │   ├── auth/            # Authentication
│   │   ├── products/        # Products
│   │   ├── orders/          # Orders
│   │   ├── reviews/         # Reviews
│   │   ├── deals/           # Deals
│   │   ├── users/           # Users
│   │   ├── stats/           # Statistics
│   │   ├── middleware/      # Middleware
│   │   │   ├── verifyToken.js
│   │   │   ├── virifyAdmin.js
│   │   │   └── generateToken.js
│   │   └── utils/           # Utilities
│   │       ├── uploadImage.js
│   │       └── globalLimiter.js
│   ├── index.js             # Entry point
│   └── package.json
│
├── er-diagram.puml          # Database ER diagram
├── use-case.puml            # Use-case diagram
└── README.md                # Documentation
```

## 🚀 Installation & Setup

### Prerequisites

- Node.js (version 18 or higher)
- npm or yarn
- MongoDB (local or MongoDB Atlas)
- Cloudinary account (for image uploads)
- Stripe account (for payments)

### Step 1: Clone the repository

```bash
git clone <repository-url>
cd "LEBABA Shop"
```

### Step 2: Install Backend dependencies

```bash
cd backend
npm install
```

### Step 3: Configure Backend environment variables

Create a `.env` file in the `backend/` folder with the following content:

```env
PORT=5000
DATABASE=mongodb://localhost:27017/lebaba-shop
# or for MongoDB Atlas:
# DATABASE=mongodb+srv://username:password@cluster.mongodb.net/lebaba-shop

JWT_SECRET=your-secret-jwt-key-here
CLOUDINARY_CLOUD_NAME=your-cloudinary-cloud-name
CLOUDINARY_API_KEY=your-cloudinary-api-key
CLOUDINARY_API_SECRET=your-cloudinary-api-secret
STRIPE_SECRET_KEY=your-stripe-secret-key
```

### Step 4: Start Backend

```bash
npm start
```

Backend will be available at `http://localhost:5000`

### Step 5: Install Frontend dependencies

Open a new terminal:

```bash
cd frontend
npm install
```

### Step 6: Configure Frontend environment variables

Create a `.env` file in the `frontend/` folder with the following content:

```env
VITE_API_URL=http://localhost:5000
VITE_STRIPE_PUBLISHABLE_KEY=your-stripe-publishable-key
```

### Step 7: Start Frontend

```bash
npm start
```

Frontend will be available at `http://localhost:5173`

## 🔌 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /auth-check` - Authorization check

### Products
- `GET /api/product` - Get all products (with filtering)
- `GET /api/product/:id` - Get product by ID
- `POST /api/product` - Create product (admin only)
- `PUT /api/product/:id` - Update product (admin only)
- `DELETE /api/product/:id` - Delete product (admin only)

### Orders
- `GET /api/order` - Get user orders
- `GET /api/order/:id` - Get order by ID
- `POST /api/order` - Create order
- `PUT /api/order/:id` - Update order status (admin only)

### Reviews
- `GET /api/review/:productId` - Get product reviews
- `POST /api/review` - Create review
- `PUT /api/review/:id` - Update review
- `DELETE /api/review/:id` - Delete review

### Deals
- `GET /api/deal` - Get all deals
- `POST /api/deal` - Create deal (admin only)
- `PUT /api/deal/:id` - Update deal (admin only)
- `DELETE /api/deal/:id` - Delete deal (admin only)

### Statistics
- `GET /api/stats` - Get statistics (admin only)

### Users
- `GET /api/users` - Get all users (admin only)
- `GET /api/users/:id` - Get user by ID
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user (admin only)

### Image Upload
- `POST /uploadImage` - Upload image to Cloudinary

## 💡 Functionality

### Authentication System
- Secure registration with password hashing (bcrypt)
- JWT tokens for authorization
- Protected routes for administrators
- Access control via middleware

### Product Management
- CRUD operations for products
- Image uploads to Cloudinary
- Product filtering and search
- Categories and tags
- Rating system

### Cart & Orders
- Cart persistence in localStorage
- Order placement
- Order status tracking
- Stripe payment integration

### Review System
- Leave reviews on products
- Edit and delete own reviews
- Product rating display

### Admin Panel
- Manage products, orders, and users
- Sales and order statistics
- Data visualization with charts
- Deals management

## 🌐 Deployment

The project is configured for deployment on Vercel. Configuration files are located in:
- `frontend/vercel.json`
- `backend/vercel.json`

### Deploy to Vercel:

1. Install Vercel CLI:
```bash
npm i -g vercel
```

2. Deploy Backend:
```bash
cd backend
vercel
```

3. Deploy Frontend:
```bash
cd frontend
vercel
```

Remember to configure environment variables in the Vercel dashboard for each project.

## 🔒 Security

- Helmet for HTTP header protection
- Rate limiting for DDoS protection
- Sanitization for NoSQL injection protection
- XSS protection
- JWT tokens for secure authorization
- Password hashing with bcrypt
- CORS configuration

## 📊 Diagrams

The project includes two diagrams:
- `er-diagram.puml` - Database structure ER diagram
- `use-case.puml` - Use-case diagram for usage scenarios

Use PlantUML or an online editor to view the diagrams.

## 👤 Author

LEBABA Shop Development Team

## 📝 License

ISC

---

**Happy shopping! 🛍️**
