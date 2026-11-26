# SAKKAF — Product Requirements

## Overview

SAKKAF is a traditional coffee and tea company. The brand sells carefully sourced single origin coffees from around the world, alongside traditional coffee and tea blends, with a focus on craft, origin, and heritage.

**Tagline:** A traditional coffee and tea company, rooted in craft and origin.

**Positioning note:** SAKKAF is a global coffee and tea company. The regional focus applies to the **blends only** — not to the brand as a whole or to single origin coffees.

## Brand

### Logo

- **Wordmark:** SAKKAF (uppercase)
- **Subtitle:** Coffee & Tea

### Visual identity

The bag's near-black, gold and cream, with the double gold rule. No product photography and no product listings before launch.

| Token | Value     | Usage                          |
| ----- | --------- | ------------------------------ |
| Ink   | `#0f100f` | Page background                |
| Gold  | `#d9b537` | Logo, headlines, rules, buttons |
| Cream | `#f6f0d4` | Body type and cards            |

- **Logo:** S mark with steam stroke, and the matching SAKKAF wordmark (`assets/`).
- **Typeface:** Cinzel for headings. Jost for body text, navigation and buttons.
- **Tone:** Direct and in-house. Roasted and blended to order.

## Products

### Core offerings

| Category               | Description                                                             |
| ---------------------- | ----------------------------------------------------------------------- |
| Single origin coffees  | Coffees sourced from specific regions and growers **worldwide**         |
| Coffee blends          | **Traditional** blends from the Middle East, North Africa, and Africa |
| Tea blends             | **Traditional** blends from the Middle East, North Africa, and Africa |

### Examples

- Saudi coffee (coffee blend)
- Moroccan coffee (coffee blend)

### Messaging guidelines

- Lead with SAKKAF as a traditional coffee and tea company.
- Describe single origins as global — sourced from around the world.
- Describe coffee and tea blends as traditional recipes from the Middle East, North Africa, and Africa.
- Do not frame the entire company as Middle Eastern or North African.

## Infrastructure

| Service  | Details                                                                 |
| -------- | ----------------------------------------------------------------------- |
| Domain   | [www.sakkaf.com](https://www.sakkaf.com)                                |
| Hosting  | Vercel (`com.sakkaf`)                                                   |
| GitHub   | [superdoopertrooper/com.sakkaf](https://github.com/superdoopertrooper/com.sakkaf) |
| Database | Supabase (`hklvpjnfusupxtnltrds`)                                     |

### Repository layout

```
index.html              # Coming-soon landing page
api/subscribe.js        # Mailing list signup (Vercel serverless)
supabase/migrations/    # Database migrations
package.json            # @supabase/supabase-js dependency
.env.example            # Local env template (copy to .env)
```

## Site — current (v0)

Static coming-soon landing page deployed to **www.sakkaf.com**.

### Shipped

- [x] Brand lockup in the bag's black and gold, with the S mark
- [x] Support page with contact form (`/support`)
- [x] Product category summary and site copy
- [x] Social links (TikTok, Instagram, YouTube, Facebook)
- [x] Mailing list signup form with success/error feedback
- [x] `/api/subscribe` Vercel serverless function
- [x] Supabase `mailing_list_subscribers` table (RLS enabled)
- [x] Vercel env vars (`SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`)
- [x] GitHub repo connected to Vercel for deploys
- [x] Supabase MCP configured in `.cursor/mcp.json`

### Site copy (v0)

**Tagline**

> A traditional coffee and tea company, rooted in craft and origin.

**Body**

> We source single origin coffees from around the world. Our coffee and tea blends are traditional recipes from the Middle East, North Africa, and Africa. Our online shop is opening soon.

**Product line**

> Single Origin Coffees · Coffee Blends · Tea Blends

**Mailing list**

> Join the mailing list — Be first to know when our shop opens.

## Backend — Supabase

- **Project:** [hklvpjnfusupxtnltrds](https://supabase.com/dashboard/project/hklvpjnfusupxtnltrds)
- **URL:** `https://hklvpjnfusupxtnltrds.supabase.co`

### Schema

**`mailing_list_subscribers`**

| Column       | Type        | Notes                    |
| ------------ | ----------- | ------------------------ |
| `id`         | `uuid`      | Primary key              |
| `email`      | `text`      | Unique, required         |
| `created_at` | `timestamptz` | Defaults to `now()`    |

- RLS enabled; writes go through `/api/subscribe` using the service role key
- Migration: `supabase/migrations/001_mailing_list.sql`
- Apply future migrations via Supabase MCP `apply_migration` (server: `project-0-com.sakkaf-supabase`)

### Environment variables

| Variable                    | Where        | Purpose                          |
| --------------------------- | ------------ | -------------------------------- |
| `SUPABASE_URL`              | Vercel, `.env` | Supabase project URL           |
| `SUPABASE_SERVICE_ROLE_KEY` | Vercel, `.env` | Server-side mailing list writes |
| `SUPABASE_ANON_KEY`         | `.env` only  | Optional, for future client use  |

## Site — planned features

### Phase 1 — Launch

- [x] **Mailing list storage** — Signups saved to Supabase
- [ ] **Mailing list notifications** — Email subscribers when the shop opens
- [ ] **Our story** — Company heritage, sourcing philosophy, and values
- [ ] **Coffee growers** — Partner farms and origins behind single origin coffees

### Phase 2 — Commerce

- [ ] **Product catalog** — Single origin coffees, plus traditional coffee and tea blends from the Middle East, North Africa, and Africa
- [ ] **Cart** — Add to cart, quantity, and cart summary
- [ ] **Stripe integration** — Checkout, payments, and order confirmation
- [ ] **Cross-sell** — Related blends and single origins by region on product and cart pages

## Content pages (planned)

| Page           | Purpose                                               |
| -------------- | ----------------------------------------------------- |
| Home           | Brand introduction and featured products              |
| Shop           | Browse products by category                           |
| Our Story      | Company history and values                            |
| Growers        | Origin stories and partner farms                      |
| Product detail | Origin notes, tasting profile, brew guidance, pricing |

## Social

- TikTok: [@sakkaf.com](https://www.tiktok.com/@sakkaf.com)
- Instagram: [@sakkaf_coffee](https://www.instagram.com/sakkaf_coffee)
- YouTube: [@sakkaf_coffee](https://www.youtube.com/@sakkaf_coffee)
- Facebook: [Sakkaf](https://www.facebook.com/people/Sakkaf/61590856212764)

## Open questions

- Email provider for shop-launch notifications (Resend, Mailchimp, etc.)
- Product photography and copy for launch catalog
- Shipping regions and fulfillment partner
