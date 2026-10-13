# Sellable Barbershop Website — Option A starter

This is a starter template for selling a **separate website to each business owner**. Each buyer should have their own Supabase project, so their login, business settings, services, and booking data are kept separate from other buyers.

## Files
- `index.html` — customer website + owner login/dashboard, with a blue/white/mulberry palette, animated barber pole, subtle motion, and reduced-motion accessibility support.
- `supabase/schema.sql` — tables, row-level security policies, and automatic business profile creation.
- `README.md` — beginner setup and deployment guide.

## Important limitations before selling
This is a starter, not a fully audited commercial SaaS product. Test it with dummy data first. Public booking forms can be abused by bots; before production, add rate limiting/CAPTCHA, backups, monitoring, and a tested support/recovery process. Email confirmation and password reset should be configured in Supabase. Use current legal advice for Ghana's data protection requirements and publish a privacy notice/terms. Do not promise legal compliance just because these features are present.

**Payment processing is not integrated.** The customer-facing payment note is informational only. Never ask for MoMo PINs or store payment-provider secret keys in `index.html`. To integrate Paystack or another provider, use the buyer's own merchant account and a secure server/edge function to create and verify transactions. Verify payment status server-side before confirming an appointment.

## Beginner setup (each buyer gets a separate project)
1. Create a Supabase account at https://supabase.com/ and create a new project for the buyer. Choose a strong database password and keep it private.
2. Open the project's **SQL Editor**. Copy all of `supabase/schema.sql` into a new SQL query and run it. Check that it completes without errors.
3. In Supabase **Authentication → URL Configuration**, set the site URL to the deployed website URL. Add your deployed domain and any test domain to the allowed redirect URLs. Configure email confirmation and password reset.
4. Find the project's **Project URL** and **publishable/anon key** in the API settings. These public client values are intended for browser use when row-level security is correctly enabled. Never use the `service_role` or secret key in this website.
5. Open `index.html` in a text editor. Replace:
   - `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE`
   - `PASTE_YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY_HERE`
   with this buyer's own Project URL and public/publishable key. Do not add any secret key.
6. Upload `index.html` to the buyer's own GitHub repository as `index.html`, then enable GitHub Pages in the repository settings. For easier editing, use a code editor rather than editing the file inside a phone browser. GitHub Pages hosts static files only; it does not keep private server secrets.
7. Open the deployed website, choose **Owner login → First-time owner registration**, and register the buyer's email and a unique password of at least 12 characters. Confirm the email if requested, then sign in.
8. In the owner dashboard, set the real business name, phone, WhatsApp, address, hours, map link and public payment note. Add the shop's real services/prices.
9. Test with dummy data: customer booking submission; owner sign-in; owner sign-out; another account cannot access the first owner's settings; anonymous visitors cannot read booking records. If any check fails, do not launch.
10. For the next buyer, create a completely new Supabase project and website deployment. Never reuse a buyer's database or keys for another business.

## Data/privacy practices
- Collect only what is needed to manage an appointment.
- Publish a privacy notice stating who operates the shop/site, why contact details are collected, how long records are retained, how to request access/deletion, and how to contact the business.
- Restrict who can access the owner email and booking records; use MFA for owner email where possible.
- Do not collect national ID, card details, MoMo PIN, or other unnecessary sensitive data.
- Decide and document retention/deletion, backups, incident response, and who is responsible for customer data.
- Check applicable Ghanaian law and Data Protection Commission requirements with a qualified local professional before commercial launch.

## Pricing / cost
Supabase and GitHub Pages have free tiers, but quotas, terms and availability can change. A custom domain, email delivery, backups, anti-spam, payment integrations and ongoing maintenance may cost money. Check current plan limits before selling; never guarantee that a production service will remain free.

## Security notes
- The dashboard uses Supabase Auth; no hard-coded admin passcode.
- Database row-level security (RLS) is essential. Do not disable it.
- Browser-visible project URL/public key are not passwords. Access must be constrained by RLS.
- Never expose a Supabase service-role key, Paystack secret key, database password, or email-provider secret in frontend code.
- A buyer's site should use their own domain/account, or your written license should clearly state who controls renewals and data export.
