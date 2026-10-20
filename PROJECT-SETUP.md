# Cozy Cube — Booking Setup (Staging Only)

## Confirmed business settings
- Business: Cozy Cube
- Area: Bahria Town (confirm which city/phase to display publicly)
- Stay length: 12 hours
- Maximum guests: 4
- WhatsApp: `+92 320 0432875` (provided as `03200432875`)
- Booking email: `cozycubee@gmail.com`
- Apartments: multiple
- Price: not decided
- Launch: keep unpublished until testing and explicit approval

## What is included in this package
- `booking.html`: responsive booking-request prototype matching the existing site's cream/green palette and Manrope/DM Sans typography.
- `PROJECT-SETUP.md`: recommended architecture, missing details, and production checklist.
- `README.md`: package overview.

The page has temporary apartment options, customer details, a preferred date/time, guest limit of four, and WhatsApp/email draft links. It does not store the form or check availability. Do not accept live bookings through this prototype.

## Recommended architecture

1. **Keep the existing GitHub repository for source control.**
2. **Supabase** for PostgreSQL database and admin authentication. Tables should represent apartments, booking requests, and decision history.
3. **Server-side Edge Function** for validating requests and sending admin notifications. Do not trust the browser alone for approval, availability, or price.
4. **Email**: start with manual email draft/contact; for automatic notifications, connect an email delivery provider (e.g. Resend) from a server-side function.
5. **WhatsApp**: initially use the click-to-chat link. For automatic notifications, WhatsApp Business Platform/Cloud API and its approved setup are needed.
6. **Staging only**: use a non-public preview environment. Do not enable GitHub Pages or publish a public URL until explicitly approved.

## Missing business decisions

- Exact city/phase/address wording for Bahria Town; avoid publishing a private unit address.
- Actual apartment names/IDs, descriptions, photos, capacity per apartment, amenities, and whether all options share the same price.
- Price for each apartment for a 12-hour stay; taxes/extra fees if any.
- Check-in hours and whether requests can be submitted same-day.
- Booking policies: cancellation, late checkout, visitor/guest rules, ID requirements, payment/deposit method, and refund policy.
- Admin staff email(s) and who is authorized to approve/reject.
- Privacy notice and how long customer data should be retained.
- Whether the admin should receive notifications by email only, WhatsApp only, or both.

## Credentials and accounts needed later

Do not paste passwords or private API secrets into chat or a public repository.

- A Supabase project created under your own account. Project URL and publishable/anon key may be configured in the frontend when protected by correct Row Level Security; secret/service-role keys must remain server-side.
- An admin user created inside Supabase Auth. Do not hardcode an admin password in HTML.
- For automatic email: an email-provider account and API key stored as a server-side secret.
- For automatic WhatsApp messages: Meta Business/WhatsApp Business Platform setup, approved phone number, and access token stored as a server-side secret.
- GitHub integration currently returned a 403 when attempting to create a working branch, so repository writes need working GitHub App permissions or a manual upload/push from your own GitHub account.

## Booking states and security rules

- `Pending`: customer request received, awaiting review.
- `Approved`: admin confirms availability and explicitly approves.
- `Rejected`: admin declines the request.
- Only authenticated, authorized admins can change a request's status.
- Customers must not be able to read other customers' booking records.
- Enforce max guest count, valid date/time, apartment existence, and server-side status changes.
- Prevent overlapping approved bookings for the same apartment and time range.
- Keep audit timestamps for creation and decisions.

## Before launch checklist

- Replace temporary apartment labels with real inventory.
- Decide prices and policies.
- Build database schema, secure admin sign-in, role checks, and admin dashboard.
- Implement server-side notifications and request persistence.
- Test mobile layout, invalid form inputs, overlapping dates, admin approval/rejection, email/WhatsApp flows, and access control.
- Review privacy/data retention wording.
- Explicitly approve publishing only after staging tests pass.

## Official documentation
- Supabase docs: https://supabase.com/docs
- Supabase Auth: https://supabase.com/docs/guides/auth
- Supabase Row Level Security: https://supabase.com/docs/guides/database/postgres/row-level-security
- GitHub Pages overview: https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages
