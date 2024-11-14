# 💰 Modern Financial Dashboard

A comprehensive financial management platform built with Next.js 14, featuring bank integrations, transaction management, and detailed analytics.

![Next JS](https://img.shields.io/badge/Next.js%2014-black?style=flat&logo=next.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind-38B2AC?style=flat&logo=tailwind-css&logoColor=white)

## 🌟 Key Features

### 💼 Core Financial Features
- **📊 Interactive Dashboard**
  - Real-time financial overview
  - Multiple chart visualizations
  - Customizable date ranges
  - Account-specific filtering

- **💹 Transaction Management**
  - Detailed transaction table
  - Bulk operations (delete, categorize)
  - Advanced search functionality
  - CSV import support
  - Income/Expense categorization

- **🏦 Banking Integration**
  - Plaid bank connections
  - Real-time account syncing
  - Safe disconnection process
  - Multi-account support

### 💫 Premium Features
- **💳 Premium Subscription**
  - Lemon Squeezy integration
  - Subscription management
  - Premium analytics
  - Advanced features unlock

### 🛠️ Technical Features
- **🔒 Authentication & Security**
  - Clerk Authentication (Core 2)
  - Protected routes
  - Secure API endpoints

- **🎯 API & Data Management**
  - Hono.js API framework
  - Tanstack React Query for state
  - Drizzle ORM for database
  - PostgreSQL backend

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- PostgreSQL
- Plaid Developer Account
- Clerk Account
- Lemon Squeezy Account

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/finance-dashboard.git
cd finance-dashboard
```

2. **Install dependencies**
```bash
pnpm install
```

3. **Set up environment variables**
```bash
# .env.local
# Core
DATABASE_URL="postgresql://..."
NEXT_PUBLIC_APP_URL="http://localhost:3000"

# Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=

# Banking
PLAID_CLIENT_ID=
PLAID_SECRET=
PLAID_ENV="sandbox"

# Payments
LEMON_SQUEEZY_API_KEY=
LEMON_SQUEEZY_WEBHOOK_SECRET=
```

4. **Initialize the database**
```bash
pnpm db:push
```

5. **Start development server**
```bash
pnpm dev
```

```

## 💎 Features In Detail

### 📊 Dashboard Components

```typescript
// Example of a chart component with type switching
export function TransactionChart({ 
  type = 'bar',
  data,
  dateRange 
}: ChartProps) {
  const chartTypes = {
    bar: BarChart,
    line: LineChart,
    pie: PieChart
  };

  const ChartComponent = chartTypes[type];
  
  return (
    <Card>
      <CardHeader>
        <CardTitle>Transaction Overview</CardTitle>
        <ChartTypeSwitch value={type} onChange={setType} />
      </CardHeader>
      <CardContent>
        <ChartComponent data={data} />
      </CardContent>
    </Card>
  );
}
```

### 💳 Plaid Integration

```typescript
// Bank account connection setup
export async function connectBank(userId: string) {
  const plaidClient = new PlaidClient({
    clientId: process.env.PLAID_CLIENT_ID!,
    secret: process.env.PLAID_SECRET!,
    env: process.env.PLAID_ENV as Environment
  });

  const { link_token } = await plaidClient.linkTokenCreate({
    user: { client_user_id: userId },
    client_name: 'Finance Dashboard',
    products: ['transactions'],
    country_codes: ['US'],
    language: 'en'
  });

  return link_token;
}
```

### 📝 Transaction Management

```typescript
// Bulk transaction operations
export async function bulkDeleteTransactions(ids: string[]) {
  const result = await db.transaction(async (tx) => {
    return await tx.delete(transactions)
      .where(inArray(transactions.id, ids));
  });
  
  await invalidateQueries(['transactions']);
  return result;
}
```

### 💰 Premium Features

```typescript
// Premium subscription hooks
export function usePremiumFeatures() {
  const { subscription } = useSubscription();
  
  return {
    isEnabled: subscription?.status === 'active',
    features: {
      bulkOperations: true,
      advancedAnalytics: true,
      customCategories: true,
      dataExport: true
    }
  };
}
```

## 🔒 Security Measures

- **Authentication**
  - Clerk Core 2 integration
  - JWT validation
  - Protected API routes

- **Data Security**
  - Encrypted bank credentials
  - Secure webhook handling
  - Rate limiting
  - Input validation

## 🎯 API Endpoints

```typescript
// Example Hono.js API routes
const app = new Hono();

app.post('/api/transactions', async (c) => {
  const data = await c.req.json();
  // Handle transaction creation
});

app.get('/api/analytics', async (c) => {
  // Return analytics data
});
```

## ⚡ Performance Optimizations

- React Query for efficient data fetching
- Dynamic imports for code splitting
- Edge runtime support
- Database query optimization
- Caching strategies

## 📈 Monitoring & Analytics

- Transaction metrics
- User engagement tracking
- Error reporting
- Performance monitoring
- Usage statistics

## 🚀 Deployment

1. **Database Setup**
```bash
# Setup PostgreSQL
pnpm db:push
```

2. **Environment Configuration**
```bash
# Configure production environment
vercel env pull
```

3. **Deploy**
```bash
vercel deploy
```

## 🔄 Updates & Maintenance

- Regular dependency updates
- Security patches
- Feature additions
- Bug fixes
- Performance improvements

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgments

- [Next.js](https://nextjs.org/)
- [TailwindCSS](https://tailwindcss.com/)
- [Shadcn UI](https://ui.shadcn.com/)
- [Clerk](https://clerk.dev/)
- [Plaid](https://plaid.com/)
- [Lemon Squeezy](https://lemonsqueezy.com/)
- [Hono](https://hono.dev/)
- [Tanstack Query](https://tanstack.com/query)
- [Drizzle ORM](https://orm.drizzle.team/)

---

Built with 💙 by Awais Raza
