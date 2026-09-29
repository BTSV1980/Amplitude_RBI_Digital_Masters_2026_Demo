# Flammwerk – Amplitude demo (Digital Masters 2026)

Project: **Amplitude_DigitalMasters2026** · Org 139451 · Project 869827 (US cluster)
Historical data: 30 days (30 Aug – 29 Sep 2026), 4,200 users, 27,613 events — already uploaded.

## Deploy to GitHub Pages
1. Create a repo (e.g. `flammwerk-demo`) and upload `index.html` and `.nojekyll` to the root.
2. Settings → Pages → Deploy from branch → `main` / root. URL: `https://<user>.github.io/flammwerk-demo/`
3. Open it once and check Amplitude → Live Events for `Landing Page Viewed`.

Demo helpers: `?reset` (fresh user, Guide + Survey show again) · tap the logo 5× · Profil → "Demo zurücksetzen".
Simulate a source live: `?utm_source=chatgpt.com`, `?utm_source=instagram&utm_medium=paid_social`, `?utm_source=google&utm_medium=cpc`.

## Taxonomy

| Stage | Event | Key properties |
|---|---|---|
| Acquisition | `Landing Page Viewed` | `traffic_source` (Google, Google Ads, Instagram, Facebook, TikTok, Direct, Newsletter, ChatGPT, Perplexity, Gemini), `traffic_medium`, `is_ai_referral`, `landing_page_path`, `utm_*`, `referring_domain` |
| Browse | `Offers Viewed`, `Menu Item Viewed`, `Menu Category Viewed`, `Menu Item Added` | `product_name`, `product_category`, `price_eur` |
| Sign-up | `Sign Up Started`, `Account Created` | `signup_method` (E-Mail, Apple, Google) |
| Onboarding (Guide) | `Onboarding Started`, `Onboarding Step Viewed`*, `Onboarding Step Completed`, `Onboarding Skipped`*, `Onboarding Completed` | `step_number` 1–5, `step_name`, `skipped_at_step` |
| Onboarding actions | `Location Permission Granted` / `Denied`, `Restaurant Selected`, `Coupon Activated`, `Payment Method Added` | `permission_source` / `selection_source` / `activation_source` = onboarding |
| First order | `Order Started`, `Payment Failed`*, `Order Completed`, `Coupon Redeemed` | `is_first_order`, `order_type`, `order_value_eur`, `$revenue`, `coupon_used`, `payment_method` |
| Survey | `First Experience Survey Shown`*, `First Experience Survey Submitted`*, `First Experience Survey Dismissed`* | `rating` 1–5, `feedback_text` (DE), `feedback_theme`, `sentiment`, `onboarding_status` |
| Loyalty | `App Opened`*, repeat `Order Completed`, `Loyalty Tier Reached` | `loyalty_tier`, `orders_count` |

\* historical only — live, these come from Amplitude Guides & Surveys itself.

User properties: `acquisition_channel`, `acquisition_medium`, `initial_landing_page`, `initial_utm_*`, `signup_date`, `onboarding_status`, `first_order_date`, `orders_count`, `loyalty_tier`, `favorite_restaurant`, `payment_method_saved`, `first_experience_rating`.

## Built-in stories
- **Sources:** Google organic leads, Instagram is #2 by traffic but converts worst to sign-up (~22%); AI assistants (ChatGPT/Perplexity/Gemini) grow from ~3% to ~13% of daily landing traffic over the month and convert best (~55%).
- **Onboarding:** step 2 "Standort freigeben" is the biggest drop-off. Completed onboarding → ~64% first order vs ~31% for drop-offs.
- **Survey:** onboarding completers rate ~4.3/5; drop-offs and users with a `Payment Failed` rate much lower. Free-text themes (Coupons, Standort, Wartezeit, Bezahlung/Stabilität) deliberately overlap with typical app-store review themes.

## Guide setup (suggested)
Trigger: event `Account Created` (or `Onboarding Started`), audience `signup_date` = today. Steps can anchor on:
`#loc-btn` (Restaurants tab, URL contains `#/restaurants`), `#restaurant-list`, `#coupon-tab-C-101`, `#hero-cta`, `#pay-add-btn` (URL contains `#/profile`), tabs `#tab-coupons`, `#tab-restaurants`, `#tab-profile`.

## Survey setup (suggested)
Trigger: `Order Completed` where `is_first_order` = true, short delay. Q1 rating 1–5 "Wie war deine erste Bestellung?", Q2 open text "Was können wir besser machen?".
