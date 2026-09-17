# FixMe Hub CRM (web)

A Vercel-ready rebuild of the desktop CRM. It uses Next.js for the app and Supabase for hosted PostgreSQL, email/password authentication, and tenant isolation.

## First deployment

1. Create a free [Supabase project](https://supabase.com/dashboard/projects), then run the entire `supabase/schema.sql` file in its SQL Editor.
2. In **Authentication → Providers → Email**, choose whether new users must confirm their email. Set the Site URL to your eventual Vercel URL after deployment.
3. Copy `.env.example` to `.env.local` and enter the project's URL and **publishable** key (never a service-role key).
4. Install Node.js 20.9+ on the development PC, run `npm install`, then `npm run dev`.
5. Push this folder to a GitHub repository and import it into Vercel. Add the two `NEXT_PUBLIC_SUPABASE_*` variables to Vercel for Production, Preview, and Development before deploying.

## Security model

Each account creates its own organization automatically. Every operational table has an `organization_id`; Supabase row-level security only permits the signed-in account to read or change its own organization's records. Database credentials are never committed because `.env.local` is ignored.

## Current MVP and next enhancements

The working MVP includes authentication, dashboard, customer management, repair-job intake, inventory, sales, expenses, and reporting. The schema also retains stock movements and audit logs for the next interface pass. Before using it for a production business, add staff invitations/roles, edit/delete screens, CSV import/export, receipt printing, automatic stock deductions, and a data migration from the old SQLite file.
