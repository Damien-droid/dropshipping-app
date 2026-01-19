# 🛍️ DropshippingApp

Plateform de dropshipping full-stack avec système de paiement intégré, gestion d'inventaire et automation de commandes. Similaire à AliDrop.

## 🚀 Stack Technologique

### Frontend
- **Next.js 14** - React framework avec SSR/SSG
- **React 18** - UI library
- **TypeScript** - Type safety
- **Tailwind CSS** - Styling
- **React Hook Form** - Gestion des formulaires
- **Stripe.js** - Intégration paiement

### Backend
- **Node.js** - Runtime JavaScript
- **Express.js** - Web framework
- **PostgreSQL** - Base de données relationnelle
- **Prisma ORM** - Database ORM
- **JWT** - Authentification
- **Stripe API** - Traitement des paiements

### DevOps
- **Docker** - Containerization
- **GitHub Actions** - CI/CD
- **Vercel** / **AWS** - Hosting

## 📋 Fonctionnalités Principales

### Authentification & Onboarding
- [x] Inscription/Login avec email
- [x] Vérification email
- [x] Profil utilisateur personnalisé
- [x] Gestion abonnement (Trial, Starter, Pro)

### Dashboard
- [x] Statistiques de ventes en temps réel
- [x] Graphiques ROI
- [x] Commandes en attente
- [x] Clients actifs
- [x] Inventaire disponible

### Paiement (Checkout)
- [x] Formulaire paiement sécurisé
- [x] Intégration Stripe
- [x] Trial à $1 USD
- [x] Conditions juridiques (T&C, Privacy, Refund)
- [x] Gestion des erreurs paiement

### Gestion Produits
- [x] Import depuis AliExpress/Suppliers
- [x] Customisation produits (prix, description, images)
- [x] Synchronisation stock temps réel
- [x] Catégorisation & Tags
- [x] Bulk upload

### Commandes
- [x] Création commandes
- [x] Suivi en temps réel
- [x] Statut automatique
- [x] Notifications client
- [x] Gestion returns

### Automation
- [x] Auto-fulfillment vers fournisseur
- [x] Synchronisation inventaire
- [x] Notifications email/SMS
- [x] Webhooks

### Analytics
- [x] Dashboards KPI
- [x] Export CSV/PDF
- [x] Prévisions de ventes
- [x] Analyse profit par produit

## 📁 Structure du Projet

```
dropshipping-app/
├── frontend/                 # Next.js application
│   ├── app/                 # Pages et layouts
│   │   ├── (auth)/         # Auth pages
│   │   ├── (dashboard)/    # Dashboard pages
│   │   └── checkout/       # Checkout page
│   ├── components/         # Composants React
│   ├── lib/               # Utilities
│   ├── public/            # Assets statiques
│   └── package.json
│
├── backend/                  # Express.js API
│   ├── src/
│   │   ├── routes/        # API routes
│   │   ├── controllers/   # Logic métier
│   │   ├── models/        # DB models
│   │   ├── middleware/    # Custom middleware
│   │   ├── services/      # Services (Stripe, etc.)
│   │   └── utils/         # Helpers
│   ├── prisma/            # Prisma schema
│   └── package.json
│
├── docs/                    # Documentation
├── .github/workflows/      # CI/CD pipelines
├── docker-compose.yml      # Docker config
└── README.md
```

## 🛠️ Installation

### Prerequisites
- Node.js >= 18
- PostgreSQL >= 14
- npm ou yarn

### Setup Local

```bash
# 1. Clone repository
git clone https://github.com/Damien-droid/dropshipping-app.git
cd dropshipping-app

# 2. Installation backend
cd backend
npm install
cp .env.example .env.local
npm run migrate

# 3. Installation frontend
cd ../frontend
npm install
cp .env.example .env.local

# 4. Démarrer développement
# Terminal 1 - Backend
cd backend && npm run dev

# Terminal 2 - Frontend
cd frontend && npm run dev
```

## 🔑 Variables Environnement

### Backend (.env.local)
```
DATABASE_URL=postgresql://user:password@localhost:5432/dropshipping
JWT_SECRET=your-secret-key
STRIPE_SECRET_KEY=sk_test_...
STRIPE_PUBLISHABLE_KEY=pk_test_...
NODE_ENV=development
PORT=3001
```

### Frontend (.env.local)
```
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_STRIPE_KEY=pk_test_...
```

## 📊 Modèles de Données (Prisma)

```prisma
model User {
  id        String    @id @default(cuid())
  email     String    @unique
  password  String
  profile   Profile?
  orders    Order[]
  createdAt DateTime  @default(now())
}

model Product {
  id          String    @id @default(cuid())
  title       String
  description String?
  price       Float
  stock       Int
  images      String[]
  orders      Order[]
}

model Order {
  id        String    @id @default(cuid())
  userId    String
  user      User      @relation(fields: [userId], references: [id])
  products  Product[]
  total     Float
  status    String    @default("pending")
  createdAt DateTime  @default(now())
}
```

## 🔄 API Endpoints

### Auth
- `POST /api/auth/register` - Inscription
- `POST /api/auth/login` - Connexion
- `POST /api/auth/logout` - Déconnexion

### Products
- `GET /api/products` - Lister produits
- `POST /api/products` - Créer produit
- `PUT /api/products/:id` - Modifier produit
- `DELETE /api/products/:id` - Supprimer

### Orders
- `POST /api/orders` - Créer commande
- `GET /api/orders/:id` - Détail commande
- `GET /api/orders` - Lister commandes

### Payments
- `POST /api/payments/create-intent` - Stripe payment intent
- `POST /api/payments/webhook` - Stripe webhook

## 🧪 Testing

```bash
# Backend tests
cd backend
npm run test

# Frontend tests
cd frontend
npm run test
```

## 📦 Deployment

### Vercel (Frontend)
```bash
npm install -g vercel
cd frontend
vercel
```

### Docker (Backend)
```bash
docker-compose up -d
```

## 🤝 Contribution

1. Fork le repository
2. Créer une branche feature (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## 📄 License

MIT License - voir [LICENSE](LICENSE) pour plus de détails.

## 👨‍💻 Support

Pour toute question ou bug, ouvrir une [GitHub Issue](https://github.com/Damien-droid/dropshipping-app/issues).

---

**Made with ❤️ by Damien-droid**
