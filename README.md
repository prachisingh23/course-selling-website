# Course Selling Website

A modern Vite + React course-selling and creator-media platform. The app is built for selling AI/video courses, showing free and paid media assets, publishing blog content, accepting donations, and managing the platform through an admin dashboard.

Repository:

```text
https://github.com/prachisingh23/course-selling-website
```

## Overview

This project is a frontend-first web application for a digital learning and creator asset business. It includes public pages for visitors, authentication for learners, a checkout flow for course payments, media discovery pages, donation flows, social proof sections, and a protected admin area.

The current course catalog includes a cinematic AI video creation course with chapters, embedded YouTube lessons, downloadable PDF resources, pricing in USD/INR, progress tracking, and enrolled-course access.

## Main Features

- Responsive public website with home, about, courses, videos, photos, blog, help, search, and support pages.
- Course catalog and course detail pages with lessons, chapters, resources, prices, ratings, and enrollment flow.
- Auth pages for login, signup, forgot password, reset password, and change password.
- User pages for enrolled courses, favorites, and saved library items.
- Checkout support through PayPal and Razorpay integrations.
- Donation pages, donor wall, live donation feed, donation modal, and floating donation widget.
- Media gallery for photos and videos with filters, categories, hashtags, preview pages, and free/paid asset states.
- Blog pages with post cards, category filters, search, comments, reading progress, related posts, and share actions.
- Admin dashboard for managing articles, products/courses, users, sales, media, images, videos, settings, and AI article generation.
- Supabase integration for authentication, data access, storage-backed media, and edge functions.
- Social stats edge function support for YouTube, Facebook, and Instagram metrics.
- Performance helpers for lazy-loaded routes, resilient imports, deferred sections, and optional enhanced visuals.

## Tech Stack

- React 18
- Vite 5
- Tailwind CSS 3
- Radix UI primitives
- Lucide React icons
- Framer Motion
- React Helmet Async
- Supabase JS
- PayPal JavaScript SDK
- Razorpay Checkout
- Cloudinary upload/media support
- ESLint

## Project Structure

```text
.
├── public/
│   ├── fonts/
│   └── llms.txt
├── src/
│   ├── components/          # Shared UI and feature components
│   ├── components/media/    # Media gallery and social media components
│   ├── components/ui/       # Reusable UI primitives
│   ├── config/              # Admin and ad configuration
│   ├── constants/           # Media catalog constants
│   ├── contexts/            # Auth and notification providers
│   ├── data/                # Static social/media data
│   ├── database/            # SQL helper scripts
│   ├── hooks/               # Custom React hooks
│   ├── lib/                 # Supabase, navigation, utilities, import recovery
│   ├── pages/               # Public and user-facing pages
│   ├── pages/admin/         # Admin dashboard pages
│   ├── services/            # Course, media, payment, favorite, social services
│   └── utils/               # Upload, animation, profile, hashtag, sanitizer helpers
├── supabase/
│   ├── functions/social-stats/
│   ├── rls_lockdown.sql
│   └── rls_remaining_public_tables.sql
├── tools/
├── plugins/
├── package.json
└── vite.config.js
```

## Pages And Routes

The app uses an internal navigation state with browser path syncing. Important routes include:

```text
/                         Home
/about                    About
/courses                  Course catalog
/course/:id               Course detail and lessons
/payment                  Checkout
/enrolled-courses         User enrolled courses
/library                  User saved library
/favorites                User favorites
/videos                   Video media page
/photos                   Photo/gallery page
/gallery                  Gallery page
/media/:type/:id          Media detail preview
/blog                     Blog listing
/blog/:id                 Blog post detail
/search/:query            Search results
/help                     Help / FAQ
/donate                   Donation page
/donors-wall              Donors wall
/login                    Login
/signup                   Signup
/forgot-password          Forgot password
/reset-password           Reset password
/change-password          Change password
/ai-video-generation-tools AI tools page
```

Admin routes:

```text
/admin                    Admin dashboard
/admin/dashboard          Dashboard
/admin/articles           Manage articles
/admin/articles/new       Create article
/admin/articles/edit/:id  Edit article
/admin/products           Manage products/courses
/admin/products/new       Create product
/admin/products/edit/:id  Edit product
/admin/images             Manage images
/admin/videos             Manage videos
/admin/media              Media library
/admin/sales              Sales
/admin/users              Users
/admin/settings           Settings
/admin/ai-generator       AI article generator
```

## Requirements

- Node.js 18 or newer
- npm
- A Supabase project if you want auth, media, admin data, and edge functions
- PayPal and/or Razorpay accounts for live payments
- Cloudinary account if using cloud uploads

## Local Setup

Install dependencies:

```bash
npm install
```

Create a local environment file:

```bash
cp .env.example .env
```

Start the development server:

```bash
npm run dev
```

Default local URL:

```text
http://localhost:3000
```

## Available Scripts

```bash
npm run dev       # Start Vite dev server on port 3000
npm run build     # Generate llms.txt if possible, then build production assets
npm run preview   # Preview production build on port 3000
npm run lint      # Run ESLint quietly
```

## Environment Variables

Use `.env.example` as the starter template.

Frontend variables:

```text
VITE_PAYPAL_CLIENT_ID=your_paypal_client_id
VITE_RAZORPAY_KEY_ID=your_razorpay_key_id
VITE_CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
VITE_CLOUDINARY_UPLOAD_PRESET=your_cloudinary_upload_preset
VITE_CLOUDINARY_FOLDER=your_cloudinary_folder
VITE_SOCIAL_STATS_FUNCTION_NAME=social-stats
```

Supabase Edge Function / backend secrets:

```text
YOUTUBE_API_KEY=your_youtube_api_key
YOUTUBE_CHANNEL_ID=your_youtube_channel_id
YOUTUBE_CHANNEL_HANDLE=@your_channel_handle
META_ACCESS_TOKEN=your_meta_access_token
FACEBOOK_PAGE_ID=your_facebook_page_id
INSTAGRAM_USER_ID=your_instagram_user_id
INSTAGRAM_USERNAME=your_instagram_username
INSTAGRAM_PUBLIC_APP_ID=your_instagram_public_app_id
```

Important:

- Keep real `.env` files out of Git.
- `VITE_*` values are exposed to the browser by design.
- Server-only secrets such as API keys and Meta access tokens should be stored in Supabase secrets or your backend environment, not in frontend code.

## Supabase

The app uses Supabase for authentication, user/profile data, media data, edge functions, and admin workflows. The client is configured in:

```text
src/lib/customSupabaseClient.js
src/lib/loadSupabaseClient.js
```

Included Supabase assets:

```text
supabase/functions/social-stats/index.ts
supabase/functions/social-stats/README.md
supabase/rls_lockdown.sql
supabase/rls_remaining_public_tables.sql
src/database/schema.sql
src/database/articles_rls.sql
```

Before production use, review and apply row-level security policies:

```sql
-- In Supabase SQL editor
-- 1. Review first
-- 2. Apply only after confirming table names and policies match your project
```

Recommended files to review:

```text
supabase/rls_lockdown.sql
supabase/rls_remaining_public_tables.sql
src/database/articles_rls.sql
```

## Social Stats Edge Function

The `social-stats` Supabase Edge Function can return live and cached social data.

It supports:

- YouTube subscriber, view, and video counts
- Latest YouTube uploads
- Facebook page follower and like counts
- Instagram follower and media counts
- Public Instagram fallback data where available
- Partial responses when one platform is not configured
- A shared cache window to reduce API calls

Deploy flow:

```bash
supabase functions deploy social-stats
```

Then configure secrets in Supabase:

```bash
supabase secrets set YOUTUBE_API_KEY=...
supabase secrets set YOUTUBE_CHANNEL_ID=...
supabase secrets set META_ACCESS_TOKEN=...
supabase secrets set FACEBOOK_PAGE_ID=...
```

Keep this frontend value if using the default function name:

```text
VITE_SOCIAL_STATS_FUNCTION_NAME=social-stats
```

## Payments

### PayPal

PayPal support is implemented in:

```text
src/services/paypalService.js
src/components/PaymentComponent.jsx
```

The PayPal SDK is loaded dynamically from the browser. Add this value to `.env`:

```text
VITE_PAYPAL_CLIENT_ID=your_paypal_client_id
```

### Razorpay

Razorpay support is implemented in:

```text
src/services/razorpayService.js
```

Frontend checkout needs:

```text
VITE_RAZORPAY_KEY_ID=your_razorpay_key_id
```

The code expects a Supabase Edge Function named:

```text
create-razorpay-order
```

For production, payment success should be verified server-side before granting access to paid content.

## Course Data

The current course data is stored client-side in:

```text
src/services/courseService.js
```

It includes:

- Course metadata
- USD and INR pricing
- YouTube lesson URLs
- Google Drive PDF resources
- Chapter completion state
- Local enrolled-course and progress tracking

If moving to a full backend flow, this service is the main place to replace static course data with Supabase or API calls.

## Media Data

Media services are handled in:

```text
src/services/mediaService.js
src/constants/mediaCatalog.js
src/utils/cloudinary.js
src/utils/hashtags.js
```

The media layer supports:

- Approved image/video queries
- Free and paid assets
- Watermarked previews
- Creator names
- Hashtag extraction
- Category and resolution inference
- YouTube URL parsing
- Cloudinary video poster helpers
- Short-lived client cache

## Admin Panel

The admin entry point is:

```text
src/pages/admin/AdminLayout.jsx
```

Admin access depends on the authenticated Supabase user, profile data, and admin checks from the auth context/config. Main admin modules:

- Dashboard
- Articles
- Products / courses
- Images
- Videos
- Media library
- Sales
- Users
- AI generator
- Settings

Admin access rules should be verified in Supabase policies before production deployment.

## Styling

Styling is based on Tailwind CSS and local component primitives.

Important files:

```text
src/index.css
index.css
tailwind.config.js
postcss.config.js
src/components/ui/
```

The UI uses responsive layouts, dark visual surfaces, animated sections, mobile bottom navigation, lazy-loaded heavy components, and reusable Radix-based controls.

## Build And Deployment

Create a production build:

```bash
npm run build
```

Preview the production build:

```bash
npm run preview
```

The app can be deployed to static hosting platforms such as:

- Vercel
- Netlify
- Hostinger static hosting
- Cloudflare Pages
- Any static server that can serve the generated `dist/` directory

For single-page app hosting, configure fallback routing so unknown paths serve `index.html`.

The repository includes:

```text
public/.htaccess
```

which can help Apache-style hosting redirect SPA routes correctly.

## Security Checklist

Before going live:

- Do not commit `.env`, API keys, service role keys, payment secrets, or OAuth credentials.
- Rotate any token that was pasted into chat, terminal history, screenshots, or shared documents.
- Apply Supabase RLS policies and test public/private table access.
- Verify payment success on the server before marking a course as purchased.
- Restrict admin routes with both frontend checks and backend/Supabase policies.
- Store server-only API keys as Supabase secrets or backend environment variables.
- Check Cloudinary upload preset permissions.
- Review CORS and allowed redirect URLs in Supabase auth settings.

## Known External Services

The frontend references these external services:

- Supabase
- PayPal
- Razorpay
- Cloudinary
- YouTube
- Facebook / Meta
- Instagram / Meta
- Google Drive embedded PDF previews

## Notes For Future Development

Useful next improvements:

- Move course catalog and enrollment state from local/static data into Supabase tables.
- Add server-side purchase verification and durable order records.
- Add an included `create-razorpay-order` Supabase function or backend route.
- Add tests for payment flows, auth guards, media queries, and admin permissions.
- Add deployment-specific documentation for the chosen hosting provider.
- Move public config values into documented environment variables where practical.
