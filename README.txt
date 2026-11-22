CLASS OF 2024 DUES PORTAL
========================

FILES
- index.html: website page
- style.css: responsive design
- script.js: Supabase authentication, member dashboard, dues, payment history, Paystack, admin tools and uploads
- supabase/handle_new_user.sql: database trigger update already applied to the connected Supabase project
- supabase/functions/admin-delete-member/index.ts: secure admin-only member deletion function already deployed to Supabase

CONNECTED SUPABASE PROJECT
URL: https://iuahqnvjhotfdnbcpkph.supabase.co
Project ref: iuahqnvjhotfdnbcpkph
The browser uses only the Supabase publishable key. Never add a service-role key or Paystack secret to these website files.

PUBLISHING
1. Upload index.html, style.css and script.js together to your web host. Keep all three in the same folder.
2. Set the website's default page to index.html.
3. In Supabase Dashboard > Authentication > URL Configuration, add your published website URL to Site URL and Redirect URLs. Add both the https URL and any www version you use.
4. In Supabase Dashboard > Authentication > Providers > Email, decide whether to require email confirmation. If enabled, members must confirm the email before signing in.
5. In Supabase Dashboard > Edge Functions > Secrets, confirm PAYSTACK_SECRET_KEY is present. Do not paste it into script.js or send it in chat.
6. In Paystack Dashboard, set the webhook URL to:
   https://iuahqnvjhotfdnbcpkph.supabase.co/functions/v1/paystack-webhook
   Configure the Paystack callback/return URL to your published website URL.
7. Test one low-value payment in Paystack test mode first. Then switch to live keys only after test mode succeeds.

FUNCTIONS ALREADY DEPLOYED
- paystack-initialize (requires a signed-in member)
- paystack-webhook (verifies Paystack signature and transaction before approving)
- admin-delete-member (requires a signed-in administrator)

IMPORTANT USAGE
- Members register with full name, phone, email and password. Sign in uses email and password.
- Monthly dues are accrued from the member's registration month through the current month. Approved payments are subtracted from the balance.
- Due date uses the configured day (default 30); for months with fewer days, the last day is used.
- Online payment options are Mobile Money and Bank Card.
- Cash and Bank Transfer submissions stay pending until an administrator approves or rejects them.
- Administrator role is controlled in the Supabase profiles table. Do not allow members to edit their own role.
- Admin dashboard can change monthly amount/due day, review payments, publish announcements, view members and remove member accounts.
- Profile pictures are uploaded to the private member-photos bucket and accessed using short-lived signed URLs.

LIMITATIONS / FINAL CHECKS
- This package is a static website; publish it on HTTPS. It does not require MySQL or a local server.
- Paystack cannot be considered live-ready until PAYSTACK_SECRET_KEY is confirmed in Edge Function secrets and the webhook is configured in Paystack.
- Supabase Auth email confirmation, password reset email delivery, and production SMTP settings depend on your Supabase Auth configuration.
- Run a full test after publishing: register a new test member, confirm email if enabled, sign in, upload a photo, submit a manual payment, approve it as admin, publish an announcement, and complete a Paystack test payment.
