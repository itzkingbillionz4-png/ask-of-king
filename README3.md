# ASK OF KING — eBook store starter

A responsive dark-tech storefront starter with account sign-up, sign-in and a customer-library placeholder.

## Important status
This is the **first build / storefront foundation**, not yet a live transactional store. The demo book cards are sample listings. Real checkout, payment confirmation, protected PDF storage, admin uploads and automatic fulfilment must be configured before accepting customers or money.

## Run locally
1. Install Node.js 20 or newer.
2. Copy `.env.example` to `.env.local`.
3. Create a Supabase project at https://supabase.com and copy the project URL and anon key into `.env.local`.
4. In Supabase Authentication settings, enable email/password sign-in and configure the site's redirect URLs.
5. Run `npm install`, then `npm run dev`.
6. Open http://localhost:3000.

## Suggested no-upfront-cost deployment
- Frontend: Cloudflare Pages or Vercel free tier (check current limits and commercial-use terms).
- Authentication/database: Supabase free tier (check current limits).
- Private eBook storage: Supabase Storage private bucket, with short-lived signed download URLs.
- Payments: a Nigerian payment provider that supports bank transfer and server-side payment verification. Provider transaction fees still apply.

## Required production work
- Add a `books` table and admin-only product management.
- Add `orders` and `order_items` tables with row-level security (RLS).
- Create payment initialization and webhook routes using a server-only secret key.
- Verify webhook signatures and confirm transaction status server-side; never trust a browser redirect or uploaded transfer receipt as proof of payment.
- On verified payment, grant the buyer access to the purchased book and generate short-lived signed URLs from a private storage bucket.
- Restrict admin operations to a verified admin role. Do not rely on hiding admin buttons in the browser.
- Add privacy policy, terms, refund policy and customer-support contact.
- Replace sample book listings with real, original eBooks and accurate descriptions.

## Security notes
- Never expose `SUPABASE_SERVICE_ROLE_KEY` or `PAYSTACK_SECRET_KEY` in client-side code.
- Do not put paid PDF files in a public folder.
- Bank transfer payments require confirmed provider verification before downloads are unlocked.


## Admin dashboard (starter)
- Visit `/admin` after signing in with an account that has `app_metadata.role = "admin"`.
- Run `supabase-schema.sql` in the Supabase SQL Editor first.
- Set the admin role only through Supabase's server-side Admin API / dashboard tooling. Never expose the service-role key in browser code.
- Uploads create unpublished drafts. Publishing is available in the dashboard.
- The browser upload relies on the SQL storage policies and private buckets in the schema.

The current admin UI is a management foundation. It does not yet include secure payment processing, buyer entitlements, order fulfilment, or signed download endpoints. Do not take live payments until those server-side pieces are implemented and tested.
