# 🚀 Setup Guide - DropshippingApp

## Quick Start with Docker

The easiest way to get started is using Docker and Docker Compose.

### Prerequisites
- Docker & Docker Compose installed
- Git installed

### Steps

1. **Clone the repository**
```bash
git clone https://github.com/Damien-droid/dropshipping-app.git
cd dropshipping-app
```

2. **Copy environment variables**
```bash
cp .env.example .env.local
```

3. **Start all services**
```bash
docker-compose up -d
```

That's it! Your services are now running:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:3001
- **Database**: localhost:5432

## Manual Setup (Without Docker)

### Backend Setup

1. **Navigate to backend directory**
```bash
cd backend
```

2. **Install dependencies**
```bash
npm install
```

3. **Setup PostgreSQL database**
```bash
# Create database
psql -U postgres -c "CREATE DATABASE dropshipping_dev;"

# Run migrations
npm run migrate
```

4. **Start backend server**
```bash
npm run dev
# Server running on http://localhost:3001
```

### Frontend Setup

1. **Navigate to frontend directory**
```bash
cd frontend
```

2. **Install dependencies**
```bash
npm install
```

3. **Start development server**
```bash
npm run dev
# App running on http://localhost:3000
```

## Database Setup

### Using PostgreSQL

```bash
# Connect to PostgreSQL
psql -U dropshipping_user -d dropshipping_dev

# Run migrations
npm run prisma:migrate

# Seed database (optional)
npm run seed
```

### Prisma Commands

```bash
# Generate Prisma client
npm run prisma:generate

# Create migration
npm run prisma:migrate -- --name <migration_name>

# Reset database
npm run prisma:reset
```

## API Endpoints

Base URL: `http://localhost:3001/api`

### Authentication
- `POST /auth/register` - User registration
- `POST /auth/login` - User login
- `POST /auth/logout` - User logout

### Products
- `GET /products` - List all products
- `POST /products` - Create new product
- `GET /products/:id` - Get product details
- `PUT /products/:id` - Update product
- `DELETE /products/:id` - Delete product

### Orders
- `POST /orders` - Create order
- `GET /orders` - List orders
- `GET /orders/:id` - Get order details
- `PUT /orders/:id` - Update order status

### Payments
- `POST /payments/intent` - Create payment intent
- `POST /payments/webhook` - Stripe webhook handler

## Environment Variables

Required environment variables are listed in `.env.example`.

### Key Variables
- `DATABASE_URL` - PostgreSQL connection string
- `JWT_SECRET` - JWT signing secret
- `STRIPE_SECRET_KEY` - Stripe API secret key
- `STRIPE_PUBLISHABLE_KEY` - Stripe public key
- `NODE_ENV` - Environment (development/production)

## Development Commands

### Backend
```bash
cd backend

# Run dev server
npm run dev

# Run tests
npm run test

# Lint code
npm run lint

# Format code
npm run format
```

### Frontend
```bash
cd frontend

# Run dev server
npm run dev

# Build for production
npm run build

# Run tests
npm run test

# Lint code
npm run lint
```

## Troubleshooting

### Port Already in Use
```bash
# Kill process on port 3000
lsof -ti :3000 | xargs kill -9

# Kill process on port 3001
lsof -ti :3001 | xargs kill -9
```

### Database Connection Error
```bash
# Ensure PostgreSQL is running
# Update DATABASE_URL in .env.local
# Check credentials in docker-compose.yml
```

### Module Not Found
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

## Production Deployment

See [DEPLOYMENT.md](./DEPLOYMENT.md) for production setup instructions.

## Support

For issues or questions, please open a GitHub issue.
