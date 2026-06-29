# Medi Store Frontend

A Next.js 16.2.9 + TypeScript storefront for the MediStore medicine marketplace.

## Live Deployment

- Frontend: [https://medi-store-front-end-alpha.vercel.app](https://medi-store-front-end-alpha.vercel.app)
- Backend API proxy: [https://medi-store-back-end-three.vercel.app/api](https://medi-store-back-end-three.vercel.app/api)

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

```medi-store-front-end-extended/
│
├── app/                              # Next.js App Router pages
│   ├── page.tsx                      # Public homepage
│   ├── layout.tsx                    # Root layout (providers, fonts)
│   ├── globals.css                   # Global styles + Tailwind v4 theme
│   ├── not-found.tsx                 # 404 page
│   ├── 403/page.tsx                  # Forbidden page
│   │
│   ├── (customer)/                   # Customer route group
│   │   ├── cart/page.tsx             # Shopping cart
│   │   ├── checkout/page.tsx         # COD + Stripe checkout flow
│   │   └── orders/
│   │       ├── page.tsx              # Order history
│   │       └── [id]/page.tsx         # Order detail
│   │
│   ├── checkout/                     # Stripe redirect landing pages
│   │   ├── success/page.tsx          # Payment success
│   │   └── cancel/page.tsx           # Payment cancelled
│   │
│   ├── shop/
│   │   ├── page.tsx                  # Medicine listing with filters
│   │   └── [id]/page.tsx             # Medicine detail + reviews
│   │
│   ├── wishlist/page.tsx             # Saved medicines
│   ├── profile/page.tsx              # User profile + edit
│   ├── login/page.tsx                # Login (Suspense-wrapped for Next.js 16)
│   ├── register/page.tsx             # Registration
│   ├── about/page.tsx                # About page
│   ├── contact/page.tsx              # Contact page
│   ├── faq/page.tsx                  # FAQ page
│   │
│   ├── seller/                       # Seller dashboard (role-protected)
│   │   ├── dashboard/page.tsx        # Stats overview
│   │   ├── medicines/page.tsx        # Manage products (CRUD)
│   │   └── orders/page.tsx           # Incoming orders
│   │
│   └── admin/                        # Admin dashboard (role-protected)
│       ├── page.tsx                  # Stats overview → /admin
│       ├── users/page.tsx            # User management (ban/unban)
│       ├── categories/page.tsx       # Category management (CRUD)
│       └── orders/page.tsx           # All orders
│
├── components/
│   ├── home/                         # Homepage sections
│   │   ├── HeroSection.tsx
│   │   ├── FeaturedMedicines.tsx
│   │   ├── CategoriesSection.tsx
│   │   ├── HowItWorks.tsx
│   │   ├── StatsSection.tsx
│   │   ├── TestimonialsSection.tsx
│   │   └── TrustBanner.tsx
│   ├── medicine/
│   │   └── MedicineCard.tsx          # Reusable medicine card
│   ├── order/
│   │   └── OrderStatusBadge.tsx      # Colour-coded status badge
│   ├── shared/
│   │   ├── Navbar.tsx                # Top navigation (role-aware)
│   │   └── Footer.tsx
│   └── ui/
│       └── Skeleton.tsx              # Loading skeleton component
│
├── context/
│   ├── AuthContext.tsx               # Auth state — localStorage + JWT
│   ├── CartContext.tsx               # Cart state — localStorage
│   └── WishlistContext.tsx           # Wishlist state — localStorage
│
├── lib/
│   ├── axios.ts                      # Axios instance + auth interceptor
│   └── utils.ts                      # cn(), formatPrice(), getErrorMessage()
│
├── types/
│   └── index.ts                      # Shared TypeScript types
│                                     # (User, Medicine, Order, Category, etc.)
│
├── public/                           # Static assets
├── proxy.ts                          # Next.js middleware — route protection
├── next.config.ts                    # Next.js config
├── tailwind.config.ts                # Tailwind config
├── tsconfig.json                     # TypeScript config
└── package.json
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

| Method | Endpoint |
| --- | --- |
| POST | `/api/auth/register` |
| POST | `/api/auth/login` |
| POST | `/api/auth/logout` |
| GET | `/api/auth/me` |

### Categories

| Method | Endpoint |
| --- | --- |
| GET | `/api/categories` |
| POST | `/api/categories` |
| PUT | `/api/categories/:id` |
| DELETE | `/api/categories/:id` |

### Medicines

| Method | Endpoint |
| --- | --- |
| GET | `/api/medicines` |
| GET | `/api/medicines/:id` |
| POST | `/api/medicines` |
| PUT | `/api/medicines/:id` |
| DELETE | `/api/medicines/:id` |

### Orders

| Method | Endpoint |
| --- | --- |
| POST | `/api/orders` |
| GET | `/api/orders/my-orders` |
| GET | `/api/orders/:id` |

### Payments

| Method | Endpoint |
| --- | --- |
| POST | `/api/payments/create-checkout-session` |

### Reviews

| Method | Endpoint |
| --- | --- |
| POST | `/api/reviews` |

### Seller

| Method | Endpoint |
| --- | --- |
| GET | `/api/seller/dashboard` |
| GET | `/api/seller/medicines` |
| POST | `/api/seller/medicines` |
| PUT | `/api/seller/medicines/:id` |
| DELETE | `/api/seller/medicines/:id` |
| GET | `/api/seller/orders` |

### Admin

| Method | Endpoint |
| --- | --- |
| GET | `/api/admin/dashboard` |
| GET | `/api/admin/users` |
| PATCH | `/api/admin/users/:id` |
| GET | `/api/admin/orders` |

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
