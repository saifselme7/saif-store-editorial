# saif-store-editorial

Bilingual English / Egyptian Arabic (RTL) fashion storefront and admin CMS built with React, TypeScript, GSAP, Lenis, Framer Motion, Zustand, and Supabase.

Live: [demo-shop1.vercel.app](https://demo-shop1.vercel.app)

## Architecture Notes

- **Motion and scroll stack:** Combines Lenis smooth scrolling with GSAP `ScrollTrigger` timelines for editorial page reveals and Framer Motion `AnimatePresence` for route and loader transitions.
- **Bilingual RTL support:** Switches between English and Egyptian Arabic with document-level `dir` handling across storefront views, cart state, and checkout flows.
- **Modular Supabase layer:** Backed by 8 sequential SQL migrations (`supabase/migrations/001` through `008`) covering catalog schema, seeding, admin authentication, RLS policies, image storage buckets, orders, hero CMS configuration, and manual payment settings.
- **Admin CMS (`/admin`):** Protected routes for managing products, categories, collections, orders, homepage hero content, manual payment configuration, and runtime Supabase connection diagnostics.

## Stack

- **Frontend:** React 18, TypeScript, Vite, React Router 6, Tailwind CSS
- **State & Motion:** Zustand, GSAP (`@gsap/react`), Lenis, Framer Motion
- **Backend:** Supabase (PostgreSQL, Auth, RLS, Storage)

## Project Structure

```text
src/
├── pages/        # Storefront pages (Home, Shop, Product, Cart, Checkout, OrderStatus) and /admin views
├── sections/     # Homepage editorial sections
├── components/   # UI primitives, layout chrome, and protected admin shell
├── services/     # Domain-level Supabase query and mutation modules
├── store/        # Zustand cart and client state stores
├── hooks/        # Lenis scroll, magnetic interactions, and viewport hooks
└── lib/          # Supabase client and utility helpers
supabase/
└── migrations/   # Numbered SQL migrations (001_saif_store_schema.sql .. 008_manual_payments.sql)
```

## Local Setup

```bash
npm install
cp .env.example .env
# Fill in VITE_SUPABASE_URL and VITE_SUPABASE_PUBLISHABLE_KEY
npm run dev
```

Apply the SQL migrations under `supabase/migrations/` in numeric order inside your Supabase project before using `/admin` or checkout.

Production build:

```bash
npm run build
npm run preview
```

## License

[MIT](./LICENSE)
