# The Betta Boutique

Premium Betta fish and aquarium storefront built with Next.js, TypeScript, Tailwind-ready CSS tokens, Prisma, Stripe Checkout architecture, Zod validation, and a local persistent guest cart.

## Quick start

```bash
npm install
copy .env.example .env
npm run dev
```

Open `http://thebettaboutique07`.

## Environment

Set `DATABASE_URL` for PostgreSQL, `AUTH_SECRET` for Auth.js, and the Stripe test keys before enabling payments. `NEXT_PUBLIC_SITE_URL` must match the environment used for Stripe redirects. `FREE_SHIPPING_THRESHOLD` can override the ₹1,999 display threshold when the database-backed settings service is added.

## Database

```bash
npm run db:generate
npm run db:migrate -- --name init
npm run db:seed
```

The seed creates catalog records across all five categories and an `admin@thebettaboutique.in` user with the `ADMIN` role. Configure an Auth.js credentials/OAuth provider before allowing this account to sign in.

## Stripe test mode

Add `STRIPE_SECRET_KEY=sk_test_...` and `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...` to `.env`. The checkout endpoint creates a server-side Stripe Checkout Session; use Stripe’s test card `4242 4242 4242 4242` on the hosted page. Add a verified webhook endpoint for `checkout.session.completed` before production and save the resulting payment/order status through Prisma.

## Commands

```bash
npm run lint
npm run typecheck
npm run build
```

## Structure

- `app/` — routes, pages, server API endpoints
- `components/` — reusable cart, header, footer and product UI
- `lib/catalog.ts` — development catalog abstraction (replace with Prisma queries)
- `prisma/` — production PostgreSQL schema and catalog seed

For production, complete the Auth.js adapter, wire the provided contact/newsletter endpoints to Prisma, configure Cloudinary image uploads, and add the Stripe webhook secret/handler. These integrations intentionally require real service credentials and are not simulated.
