# Medi Store - Frontend

A modern e-commerce platform for purchasing medicines online, built with Next.js and React.

## Tech Stack

- **Framework**: Next.js 16.2.9 with TypeScript
- **Styling**: Tailwind CSS
- **State Management**: React Context (Auth, Cart)
- **HTTP Client**: Axios
- **Payments**: Stripe
- **Validation**: Zod
- **UI Components**: Lucide React Icons, React Hot Toast
- **Linting**: ESLint

## Features

### Customer
- Browse and search medicines by category
- Add items to cart and checkout
- Complete orders via Stripe integration
- View order history and track status
- User authentication (login/register)
- Customer profile management

### Admin
- Manage medicine categories
- Monitor and manage all orders
- User management dashboard

### Seller
- Seller dashboard
- Add and manage medicines
- Track seller orders

### Public Pages
- Home with featured medicines and stats
- Shop with medicine listings
- About, Contact, and FAQ pages

## Installation

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build

# Start production server
npm start
```

## Project Structure

- `/app` - Next.js app router with page routes
- `/components` - Reusable React components (home, medicine, order, shared, ui)
- `/context` - React Context providers (Auth, Cart)
- `/lib` - Utility functions and axios configuration
- `/types` - TypeScript type definitions
- `/public` - Static assets

## Environment Setup

Create a `.env.local` file with required API endpoints and Stripe keys (if applicable).

## Development

```bash
npm run dev
```

Open https://medi-store-front-end-alpha.vercel.app to view the application.

---

**Status**: Under Development
