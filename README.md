# Medi Store Frontend

A Next.js 16.2.9 + TypeScript storefront for the MediStore medicine marketplace.

## Live Deployment

- Frontend: `https://medi-store-front-end-alpha.vercel.app`
- Backend API proxy: `https://medi-store-back-end-three.vercel.app/api`

## Tech Stack

- Next.js 16.2.9
- React 19.2.4
- TypeScript
- Tailwind CSS
- Axios
- Zod validation
- React Context for auth and cart state
- ESLint for linting

## Features

- Public home page with featured medicines, categories, and testimonials
- Shop browsing with category filters and medicine details
- Authenticated customer flows: login, register, cart, checkout, order history, profile
- Seller dashboard: manage medicines, view orders
- Admin dashboard: manage categories, users, and orders
- Route protection using Next.js middleware

## Folder Structure

```text
app/                       # Next.js app router pages and layouts
  (customer)/              # Customer-only pages (cart, checkout, orders)
  admin/                   # Admin dashboard pages
  seller/                  # Seller dashboard pages
  checkout/                # Checkout success/cancel pages
  login/                   # Login page
  register/                # Register page
  profile/                 # Customer profile page
  shop/                    # Shop listing and medicine detail pages
components/                # Reusable UI components
  home/                    # Home page sections
  medicine/                # Medicine card components
  order/                   # Order status UI
  shared/                  # Navbar, Footer, etc.
  ui/                      # Generic UI helpers like skeleton loaders
context/                   # React context providers for auth and cart
lib/                       # Axios client and utility functions
public/                    # Static assets
types/                     # Shared TypeScript types
README.md                  # Project documentation
next.config.ts             # API rewrite configuration
proxy.ts                   # Route protection middleware
```

## API Configuration

This frontend uses API rewrites and proxying to route `/api/*` requests to the backend:

- Local/production base API path: `/api`
- Backend destination: `https://medi-store-back-end-three.vercel.app/api/:path*`

The Axios client in `lib/axios.ts` is configured with:

- `baseURL: "/api"`
- `withCredentials: true`
- automatic redirect to `/login` on 401 responses

## Frontend Routes

- `/` — Home page
- `/shop` — Medicine listing page
- `/shop/[id]` — Medicine detail page
- `/login` — Login page
- `/register` — Registration page
- `/profile` — Customer profile page
- `/cart` — Cart page
- `/checkout` — Checkout page
- `/checkout/success` — Payment success page
- `/checkout/cancel` — Payment cancellation page
- `/orders` — Customer order list
- `/orders/[id]` — Order detail page
- `/seller/dashboard` — Seller dashboard
- `/seller/medicines` — Seller medicine management
- `/seller/orders` — Seller order management
- `/admin` — Admin dashboard
- `/admin/users` — Admin user management
- `/admin/orders` — Admin order management
- `/admin/categories` — Admin category management
- `/403` — Unauthorized access page

## Backend API Endpoints Used

These endpoints are consumed by the frontend through the `/api` proxy.

### Auth
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/logout`
- `GET /api/auth/me`

### Categories
- `GET /api/categories`
- `POST /api/categories`
- `PUT /api/categories/:id`
- `DELETE /api/categories/:id`

### Medicines
- `GET /api/medicines`
- `GET /api/medicines/:id`
- `POST /api/medicines`
- `PUT /api/medicines/:id`
- `DELETE /api/medicines/:id`

### Orders
- `POST /api/orders`
- `GET /api/orders/my-orders`
- `GET /api/orders/:id`

### Payments
- `POST /api/payments/create-checkout-session`

### Reviews
- `POST /api/reviews`

### Seller
- `GET /api/seller/dashboard`
- `GET /api/seller/medicines`
- `POST /api/seller/medicines`
- `PUT /api/seller/medicines/:id`
- `DELETE /api/seller/medicines/:id`
- `GET /api/seller/orders`

### Admin
- `GET /api/admin/dashboard`
- `GET /api/admin/users`
- `PATCH /api/admin/users/:id`
- `GET /api/admin/orders`

## Environment Setup

Create a `.env.local` file at the project root with values required for your environment and Stripe client keys:

```env
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
NEXT_PUBLIC_API_URL=/api
```

> The frontend uses the built-in proxy in `next.config.ts`, so API calls are forwarded to the backend automatically.

## Installation

```bash
npm install
```

## Local Development

```bash
npm run dev
```

Open `http://localhost:3000` in your browser.

## Production Build

```bash
npm run build
npm start
```

## Notes

- Route protection is implemented in `proxy.ts` using cookie-based auth and role checks.
- The app stores authenticated user info in `medistore_user` and session token in `medistore_token` cookies.
- `next.config.ts` rewrites all `/api/*` requests to the backend URL configured for deployment.

---

## Status

Production-ready frontend deployed and connected to the backend proxy.
