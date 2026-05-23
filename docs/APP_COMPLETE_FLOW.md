# Worker App

## Complete Worker Application Flow

Worker opens app. Location selection screen — allow GPS permission or manually select country then city. If GPS detects unsupported country, show error and force manual selection. Location saved locally on device. Check device language — if supported, show that language. If not, default to English. Second language option is current country's language. Splash screen with Hire Me animation while fetching data.

Check if worker exists in Clerk. If logged in, fetch profile, credits, earned credits, spent credits, videos, services, availability, reviews, everything. If not logged in, show nothing yet.

Splash finishes. If logged in, go to dashboard. If not logged in, show welcome screen with signup and login options.

Registration flow — Clerk handles Google, Facebook, email and password. If email, ask for first and last name. Show terms of use checkbox — must accept before proceeding. Clerk sends verification code via email. Worker enters code on verification screen. Code expires — can request new code. Correct code verification saves to Clerk and Supabase with one hundred free credits. Show success screen five to ten seconds with avatar, name, company name, message "Welcome to Hire Me, you earned one hundred free credits." Then redirect to onboarding.

Onboarding five steps with temp local storage saving progress:

Step one — select country from hardcoded list, then select city, add address, ZIP code optional. Country pre-filled from location selection. Temp save on next. Edit button goes back to step one.

Step two — phone, email, website, Facebook, Viber, WhatsApp. Temp save on next. Edit button goes back.

Step three — choose up to five services from database, each service has unlimited sub-services. For each service set pricing — hourly, fixed price, or by agreement. Can set different prices per sub-service. Years of experience dropdown for each service with options — 0 to 1 year, 2 to 5 years, 5 to 10 years, 10 to 20 years, 25 plus years. Temp save on next.

Step four — availability like Monday to Friday eight to five. Can set multiple availability windows. Temp save on next.

Step five — preview all data from steps one through four. Edit buttons on each section redirect to that step. Avatar from Clerk with edit button to upload new image. Accept terms of use checkbox — must check before submit. Submit button disabled until terms checked. Submit — save all data to Supabase, delete temp storage, show success screen.

Worker dashboard:

Nav bar at top — avatar on left, credits balance on right.

Profile section — avatar, name, company name, phone, email, WhatsApp, Viber icons that open dialer or messaging apps.

Views, likes, reviews section showing engagement stats. Views only count registered clients. Likes only from registered clients.

Credits section showing — total credits, earned credits breakdown (signup one hundred, first five reviews sixty, first five-star review forty), spent credits, buy credits button.

Blocks for editing with separate screens:

Location and biography block — edit button opens screen to change address, city, ZIP, biography.

Services and pricing block — edit button opens screen to change services, sub-services, pricing per service.

Availability block — edit button opens screen to change availability windows.

Media section — upload images ten credits each after five free, max fifteen images. Upload videos twenty credits each after three free, max thirty seconds per video. Image upload deducts credits only if over five free. Video upload deducts only if over three free. If at max images, can delete to upload new one. After deleting, if below five free total, next upload free. Video upload requires title, description, and tagging one service from registered services.

Promotions section — shows all videos in rows with title. Promote button for each video. Seven days promotion twenty credits or fourteen days forty credits. Verify credits before charging. Only charge if video successfully posted to feed. If already promoted, promote button disabled and three-dot menu appears to remove promotion anytime, no refund. Promotion expires end of expiration date at midnight, video drops from feed. Each video tracks own expiration date.

Reviews section — two tabs. Reviews worker left on other workers, reviews others left on worker. Each review shows rating, text, date. Can edit or delete reviews. Report button on each review. Earnings table tracks all earned credits by event type — locked in once recorded. If delete account, all reviews and earnings deleted. If register again, starts fresh.

Payments and Stripe:

Buy credits button opens payment screen. Credit packages — one hundred, three hundred, six hundred, one thousand credits. Prices in worker's registered country currency. React Native Stripe SDK for payment. Save card option. Apple Pay and Google Pay supported. Worker enters payment info or selects saved card. Only deduct credits after webhook confirms payment successful. If payment fails, show error message from Stripe, no credits added, worker can retry. Successful payment shows success message, redirects to dashboard with updated credit balance.

Login flow:

Returning workers — login with email and password, Google, or Facebook via Clerk. Or use fingerprint biometric for quick login — stored securely on device, doesn't extract actual fingerprint. Biometric fails — lock temporarily, force Clerk login. Change device — biometric doesn't work, re-authenticate with Clerk. Biometric disabled — fall back to Clerk login. Fingerprint can be set up anytime in settings.

Settings:

Change password via Clerk — only shows if registered with email and password. If Google or Facebook, hide password option. Delete account button — show confirmation "Deleting account deletes everything — reviews, earnings, videos, promotions. No recovery." Confirm, account deleted permanently with all data.

Language:

Device language detected first, if supported show it. If not, default English. Language switcher button shows second option — current country's language. Change language updates static text instantly from JSON. Services and countries translations fetched from Supabase and refresh on language change.

Countries and services:

Countries screen shows all fourteen supported countries with flag icons. Click country, redirect to cities screen showing all cities in that country. Services display with icons — hammer for construction, wrench for repairs, etcetera.

Edge cases:

Location permission denied — force manual selection.

Offline during app launch — show cached data or error.

Saved location in unsupported country — ask to pick again.

Logged in but account deleted — log out, show login screen.

Duplicate email — check by Clerk ID. One Clerk account can have multiple roles. If exists, check if worker record exists. If not, ask to register as worker.

Worker registered, comes to register again — prevent duplicate registration with message.

Promotion button tapped twice — button disabled during request, prevents duplicates.

Video deleted while promoted — warning message "Video in promotion until X date, no refund if deleted."

Video promoted, client runs out of credits — promotion continues, credits already charged upfront.

Network fails after payment but before confirmation — webhook handles retry, don't charge twice.

Video promotion expires — automatic removal from feed at end of day.

Multiple reviews — each tracks separately, can edit or delete individually.

Report abuse — admin dashboard gets report, can delete review, warn user, block account, or delete permanently.

Fingerprint fails three times — lock out temporarily, force Clerk authentication.

---

# Client App

## Complete Client Application Flow

First time client opens app — phone asks for location permission. Allow or deny. If allow, GPS detects location. If deny, manually select country then city. Location saved locally. Device language detected, if supported show it. If not, default English. Language switcher shows country language as option. Splash screen with Hire Me animation while checking Clerk login status. Splash finishes, redirect to welcome screen with three options — browse services, browse videos, register as client. Avatar top right if logged in, no avatar if not. Client can browse freely.

Second time client opens app — location already saved locally. Splash screen while checking login. Splash finishes, same welcome screen. If logged in, avatar shows. If not, no avatar. Client continues from welcome screen.

Browse services — tap services button, redirect to services screen. Shows all services with icons. Top displays registered location (country, city). Tap service, redirect to worker list screen for that service in that location. Worker list screen shows workers sorted by — active promotions first, then credit balance high to low, then star rating high to low, then distance closest first. Each worker card shows avatar, name, services, main price top corner, pricing type (hourly, fixed, by agreement). Filter icon top right of nav bar — click opens filter modal. Filter by minimum price, maximum price, distance range, experience level. Apply filters and worker list updates. Pagination loads next batch of workers as they scroll down, shows loading state. Tap worker card, redirect to worker profile. Worker profile shows avatar, name, business name, contact icons (phone with country code, WhatsApp, Viber, email), location, social media, availability, services and sub-services, reviews, report button, share button. Contact icons open dialer or messaging apps. Share opens device share menu.

Browse videos — tap videos button, redirect to video feed. Shows thirty-second promoted worker videos from their selected city, TikTok vertical scroll. Videos show worker name and service. Registered clients watch video for few seconds — increment like counter. Registered clients tap video to open worker profile — increment profile view. Only registered clients count. Same client watching same video multiple times counts each time. Like is permanent, no unlike. If registered client wants to leave review, must be logged in, prompt if not.

Languages — JSON files for static text per screen for all languages. Device language detected first, if supported. If not, default English. Language switcher shows country language as second option. Changing language updates static text instantly from JSON. Services and countries translations from Supabase refresh on language change. Services and countries show with icons and flags.

Edge cases:

Location permission denied — force manual country and city selection. Offline at launch — show cached data or error. Saved location in unsupported country — ask to pick again. No workers in location — show "No workers found." Worker contact invalid — show error when trying to contact. Client not registered trying to review — prompt to login. Client tries to like without logging in — prompt to login. Same client watching video multiple times — each like counts. Client tries to like same video twice — prevent duplicate, show already liked. Worker profile fails to load — show error or placeholder. Share button fails — show error, let retry. Auto-detect button on worker list scrolls out of view when scrolling workers — reappears when scrolling back up. Worker has no social media — don't show empty section. Video deleted while viewing — show error message. Report abuse — admin dashboard gets report. Pagination loading state shown while fetching next batch. Filter modal closes after applying filters. Filter resets to defaults if user navigates away. Worker with zero credits doesn't show promotions section. Worker with no ratings shows "No reviews yet." Distance calculation based on GPS if auto-detect used, or based on registered location otherwise.

---

# Admin Dashboard

## Complete Admin Dashboard Flow

Super admin, admin, and member login with Clerk — email and password, Google, Facebook. No registration, only super admin can add admins and members.

After login, dashboard homepage shows quick stats — total users, total workers, total clients, videos uploaded today, revenue made today, active promotions, pending reports.

Users tab — lists all users as rows with avatar, name, email. Click user, see full profile — location, services, experience level, credits balance, total spent, join date, all images, all videos, all reviews given and received, promotions history, earnings history. Admin can delete user or suspend user with note explaining why. Super admin full delete/ban access, admin limited access, member view only.

Admin management tab — visible only to super admin. Lists all admins and members with role, name, email. Super admin can add new admin or member by email, change their role, delete or remove them.

Reports tab — shows all reported users, workers, reviews with reporter info, what was reported, reason. Admin clicks report, sees full details. Can delete reported content, suspend user temporarily with note explaining why, ban user permanently, add user to blocklist. User sees "Account suspended" or "Account banned" message on login with reason. Admin can unsuspend anytime. When suspending or banning, update Supabase user status to suspended, banned, or blocked, and send request to Clerk to disable account.

Services tab — list all services with icons. Add new service with name and icon upload, edit service name or icon, delete service. Same for sub-services — add, edit, delete sub-services under each service.

Packages tab — list all credit packages (one hundred, three hundred, six hundred, one thousand credits). Add new package with credit amount and price per country, edit prices, delete package.

Promotions tab — create promotions for holidays or campaigns. Set promotion name, discount percentage, start date, end date, which services or packages apply. When active, discount applies to package prices automatically. Admin can create, edit, delete promotions.

Error logs tab — shows all user errors with timestamp, user email, device type (Android or iOS), error message, stack trace. Search by email or error type. Click error to see full details. Mark error as resolved when fixed. Errors logged when users encounter issues during registration, login, service operations. Edge functions catch errors and log to Supabase with user context and device info.

User status tracking — Supabase has user status column — active, suspended, banned, blocked. Admin actions update status and Clerk account simultaneously.

Edge cases:

Super admin password reset — Clerk handles automatically.

Two admins edit same user simultaneously — whoever saves first wins, second gets error to refresh.

Error logs get massive — paginate showing newest first, archive old errors after thirty days.

Overlapping promotions — warning shown in admin dashboard, admin decides which applies.

Admin with limited permissions tries to delete super admin — permission check prevents action.

User reported multiple times — show all reports together.

Deleted user's data — cascade delete their reviews, videos, images, earnings history.

User suspension lifted — update status in Supabase and Clerk back to active.

Blocked user tries to register with new email — identify by pattern or manual review.

Critical errors occur — logged in error tab, admin checks periodically, no automated email notifications for MVP.

Dashboard homepage responsive — works on mobile, tablet, laptop, desktop, all screen sizes.

Admin dashboard fully responsive across all devices.

---

# Backend App

## Complete Backend Application Flow

Backend serves all three apps—worker app, client app, admin dashboard. Runs locally with Docker for development using local Supabase instance. Deploys to production on Supabase Pro plan. 

Security—validate and sanitize all input server-side, never trust client data. Row Level Security policies in Supabase so users only access their own data. Workers see only their profile, videos, promotions, reviews, earnings. Clients see only their reviews, liked videos. Admins access by role—super admin full, admin limited, member view-only. 

Authentication—Clerk handles auth tokens for all apps. Token validated on every request. Expired tokens return 401 error, client refreshes token. 

Pagination—all list endpoints paginate results. Worker list loads 50 items per batch. Error logs paginate, newest first. 

Security—validate all input server-side, never trust client data. Rate limiting—limit requests per user per minute to prevent abuse and control Supabase costs. Return 429 error if exceeded, client waits before retrying. 

Caching—cache frequently accessed data like services, countries, credit packages. Short TTL like 5 minutes for changing data, longer TTL for static data. Clear cache on write so data stays fresh. 

Load testing—use k6 or Artillery to simulate hundreds or thousands of concurrent users. Run before production to identify bottlenecks. 

Stripe webhook integration—Stripe sends payment success notifications to webhook endpoint. Webhook verifies signature, checks if user exists, adds credits only after confirmed payment. If webhook fails, retry logic handles it. 

Error handling—all errors logged in error table with timestamp, user email, device type, error message, stack trace. Admin reviews errors periodically. 

Database indexes—add indexes on frequently queried columns like user ID, service ID, country for fast lookups. 

Concurrent writes—use timestamp tracking. If two admins edit same user, first save wins. 

Authentication flow—all apps use Clerk for auth. Token sent with each request, validated server-side, return 401 if invalid. 

Connection pooling—use Supabase connection pooling to manage database connections efficiently, prevent pool exhaustion. 

Async operations—long operations split into smaller batches processed asynchronously. Stripe webhook retries—failed payments retry automatically. 

RLS policies tested locally before production. Edge functions like biometric handled client-side. Input validation on all endpoints before processing.
