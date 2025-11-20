# Implementation Plan – Roy's Meal Assistant: Grocery List Companion

This document serves as a **living implementation record** for the project.  
It defines all planned and completed features, milestones, and technical steps required to reach and evolve the MVP.

---

## 🛠️ Technology Stack

**Frontend:**
- React 18+ with TypeScript
- Vite (build tool)
- Tailwind CSS (styling)
- React Hook Form + Zod (form validation)
- React Query / TanStack Query (data fetching & caching)
- React Toastify (notifications & alerts)
- Framer Motion (animations)
- Vercel (hosting & CI/CD - **Free tier**)

**Backend:**
- Node.js 20 LTS
- Express.js (REST API framework)
- TypeScript (type safety)
- Zod (request/response validation)
- JWT (authentication)
- BullMQ (background job queue)
- Sentry (error tracking - **Free tier**)
- Railway (hosting & CI/CD - **Free tier: $5/month credit**)

**Database & Cache:**
- Supabase (PostgreSQL + Auth + Real-time - **Free tier: 500MB database**)
- Redis (caching layer & job queue storage - Upstash Redis - **Free tier: 10,000 commands/day**)
- Flyway (database migrations - **Open source**)

**External Services (All Free Tier):**
- Supabase Auth (user authentication - **Free tier included**)
- Resend (transactional email - **Free tier: 100 emails/day**)
- Web Push API via Service Workers (push notifications - **Free, browser native, no third-party dependency**)
- TheMealDB API (recipe data & search - **Free tier: unlimited requests, no auth required**)

**Development & DevOps:**
- GitHub (version control & CI/CD - **Free tier**)
- GitHub Actions (automation - **Free tier: 2,000 minutes/month**)
- Docker (containerization - **Open source**)
- ESLint + Prettier (code quality - **Open source**)
- Jest + React Testing Library (testing - **Open source**)
- Vitest (unit tests for backend - **Open source**)

---

## 🤖 AI Interaction Rules

1. **Always read this file before beginning any new feature or code change.**  
   Use it to understand what features exist, their current status, and dependencies.

2. **When adding a new feature:**
   - Duplicate the "Feature Implementation Plan Model" shown below.  
   - Replace all placeholder fields (`[Feature Name]`, etc.) with real details.  
   - Insert the new feature under the appropriate section (MVP, Post-MVP, or Other).  
   - Maintain consistent formatting.

3. **When updating progress:**
   - Update the **Status** field.  
   - Check off relevant items in **Implementation Steps** and **Acceptance Criteria**.  
   - Update the **Last Updated** date.  
   - If implementation details evolve, expand the "Technical Breakdown" or "Testing Notes."

4. **When completing a major milestone (e.g., MVP deployment):**
   - Add a short summary entry at the bottom under "Development Notes" describing what changed or was achieved.

5. **Do not delete or overwrite past feature sections.**
   - Instead, mark them as "Complete" and update the timestamp.
   - This document should reflect a chronological record of development history.

---

## 📋 Feature Implementation Plan Model

Use this exact structure when creating or updating feature entries.

### Example Template

## Feature: [Feature Name]

**Purpose:**  
_Describe the intent and reason for this feature._

**User Story / Use Case:**  
_As a [user type], I want to [perform an action] so that I can [achieve benefit]._

**Dependencies / Prerequisites:**  
_List related systems, APIs, libraries, or other features required before this one can function._

**Technical Breakdown:**  
- _Frontend components/pages to build_  
- _Backend endpoints or database tables needed_  
- _Key logic or architectural notes_  

**Implementation Steps:**  
- [ ] Step 1: _Define or set up structure_  
- [ ] Step 2: _Build primary functionality_  
- [ ] Step 3: _Integrate with data sources or APIs_  
- [ ] Step 4: _Add validations/tests_  
- [ ] Step 5: _UI/UX refinements_

**Acceptance Criteria:**  
- [ ] _Feature works as intended_  
- [ ] _No errors in console/build_  
- [ ] _Responsive layout verified_  
- [ ] _Feature integrated with related systems_

**Testing & Validation Notes:**  
_Specify how to test functionality and what tools to use._

**Post-Implementation Actions:**  
_Follow-ups such as documentation, styling, or refactoring._

**Status:** Not Started / In Progress / Blocked / Complete  
**Last Updated:** YYYY-MM-DD

---

# 📌 Implementation Sections

Below are the main phases of implementation.  
Each section contains detailed feature entries that follow the Feature Implementation Plan Model above.

---

## 🎯 MVP Features
> _Core functionalities required to achieve a Minimum Viable Product._

### Feature 1: Add & Track Grocery Items with Auto-Expiration Dates

**Purpose:**  
Allow users to quickly add groceries to their inventory with automatic expiration date estimation based on item type. This reduces friction and ensures consistent date tracking without manual input.

**User Story / Use Case:**  
_As a busy home cook, I want to add groceries to my list with just a name and quantity so that the system can automatically estimate when they'll expire, saving me time and ensuring I never miss important dates._

**Dependencies / Prerequisites:**  
- User authentication system (Supabase Auth)
- Database schema for grocery items and item type expiration mappings
- Item type database (milk, eggs, bread, chicken, etc.) with default expiration days
- Frontend form validation (React Hook Form)

**Technical Breakdown:**  
- **Frontend Components:**
  - `GroceryForm.tsx` (React Hook Form + TypeScript) – Input form with item name, quantity, and optional notes
  - `GroceryList.tsx` (React Query) – Display list of all items with real-time updates
  - `GroceryCard.tsx` (Tailwind CSS) – Individual item card showing days-until-expiration with urgency colors
  
- **Backend Endpoints (Node.js + Express):**
  - `POST /api/v1/groceries` – Add new item (auto-calculates expiration based on type)
  - `GET /api/v1/groceries` – Fetch all items for authenticated user (with pagination)
  - `DELETE /api/v1/groceries/:id` – Remove item from list
  - `PUT /api/v1/groceries/:id` – Update item details
  
- **Database Tables (Supabase PostgreSQL):**
  - `groceries` (id, user_id, item_name, quantity, added_date, estimated_expiration_date, item_type, notes, created_at, updated_at)
  - `item_types` (id, type_name, default_expiration_days, category)
  
- **Key Logic:**
  - Auto-mapping item name to item_type using string fuzzy matching library (fuzzy-search)
  - Calculation: `estimated_expiration_date = added_date + item_type.default_expiration_days`
  - Data validation: Zod schema for request/response validation

**Implementation Steps:**  
- [ ] Step 1: Create database schema for groceries and item_types tables
- [ ] Step 2: Build backend endpoints (POST/GET/DELETE/PUT) with validation
- [ ] Step 3: Create frontend form component with item type selector
- [ ] Step 4: Implement auto-expiration calculation logic on backend
- [ ] Step 5: Build GroceryCard and GroceryList display components
- [ ] Step 6: Integrate with authentication system
- [ ] Step 7: Add unit tests for expiration calculation
- [ ] Step 8: UI/UX refinements (icons, colors, spacing)

**Acceptance Criteria:**  
- [ ] User can add item with name and quantity via form
- [ ] System automatically calculates expiration date based on item type
- [ ] Item appears in list with expiration date visible
- [ ] No errors in console on add/display
- [ ] Responsive on mobile, tablet, desktop
- [ ] User can delete items from list
- [ ] Expiration date persists after page refresh
- [ ] Form validation prevents empty or invalid entries

**Testing & Validation Notes:**  
- Test adding 5-10 different item types (milk, bread, eggs, chicken, etc.) and verify correct expiration dates
- Test form validation (empty fields, special characters, very long names)
- Test on mobile browser (iOS Safari, Android Chrome)
- Manual testing of database persistence
- Unit tests for expiration calculation function

**Post-Implementation Actions:**  
- Add keyboard shortcuts for quick item addition
- Create item type suggestions/autocomplete
- Implement bulk import from shopping list
- Add edit functionality for existing items

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Feature 2: Smart Grocery List Sorting

**Purpose:**  
Intelligently rank and display grocery items by three criteria: versatility (number of recipes using the ingredient), quantity on hand, and forecasted purchase needs. This helps users prioritize which ingredients to use first and understand their inventory value.

**User Story / Use Case:**  
_As a meal planner, I want my grocery list sorted by the most versatile ingredients first so that I can discover the best meals I can make with what I have, while also seeing how much of each item I possess._

**Dependencies / Prerequisites:**  
- Add & Track Grocery Items feature (Feature 1)
- Recipe API integration (Spoonacular, Edamam, or similar)
- User recipe history or saved favorites (for usage pattern analysis)
- Sorting algorithm development

**Technical Breakdown:**  
- **Frontend Components:**
  - `SortingControls.tsx` (React + Tailwind CSS) – UI toggle buttons for sorting by versatility, quantity, or forecasted needs
  - `SortedGroceryList.tsx` (React Query + useSortBy hook) – Displays groceries in selected sort order with rank badges and animations
  
- **Backend Endpoints (Node.js + Express):**
  - `GET /api/v1/groceries/sorted?sortBy=versatility|quantity|forecasted&limit=50` – Fetch sorted items with pagination
  - `GET /api/v1/recipes/ingredient-count/:itemName` – Get recipe count for ingredient (via Spoonacular API with Redis caching)
  - `GET /api/v1/groceries/usage-patterns` – Calculate forecasted needs from user history
  
- **Database Tables (Supabase PostgreSQL):**
  - Add columns to `groceries`: `recipe_count` (cached), `last_recipe_count_update`
  - `user_usage_patterns` (id, user_id, item_type, avg_usage_per_week, total_purchases, last_updated)
  - Add database index on `(user_id, item_type, created_at)` for fast query performance
  
- **External APIs & Caching:**
  - **TheMealDB API** – Free recipe database, search by ingredient, no rate limiting (free tier)
  - **Upstash Redis** – Cache recipe data (24-hour TTL) to minimize API calls; free tier: 10,000 commands/day
  
- **Key Logic:**
  - **Versatility Score:** Call TheMealDB API; store result in Upstash Redis; update `recipe_count` field
  - **Quantity Score:** Simple numeric comparison (higher quantity = lower priority in sort)
  - **Forecasted Score:** Calculate `days_until_empty = quantity / (avg_usage_per_week / 7)` from `user_usage_patterns` table

**Implementation Steps:**  
- [ ] Step 1: Integrate with Recipe API to fetch recipe counts for ingredients
- [ ] Step 2: Build backend sorting endpoints for all three criteria
- [ ] Step 3: Create sorting control UI component
- [ ] Step 4: Implement versatility scoring algorithm
- [ ] Step 5: Implement quantity-based sorting
- [ ] Step 6: Build usage pattern tracking (analyze user's past grocery additions/deletions)
- [ ] Step 7: Implement forecasting algorithm
- [ ] Step 8: Add sort persistence to user preferences
- [ ] Step 9: Unit tests for sorting algorithms
- [ ] Step 10: UI refinements (rank badges, sort icons, animations)

**Acceptance Criteria:**  
- [ ] Sorting works correctly by versatility (most versatile ingredients first)
- [ ] Sorting works by quantity (highest quantity first)
- [ ] Sorting works by forecasted needs (most urgently needed items first)
- [ ] User can toggle between sorting options via UI
- [ ] Sort preference persists across sessions
- [ ] Recipe API integration returns accurate recipe counts
- [ ] No console errors during sorting operations
- [ ] Sorting updates in real-time when items are added/removed
- [ ] Sort badges clearly display ranking number

**Testing & Validation Notes:**  
- Test sorting with 15+ items of varying types (vegetables, proteins, dairy, grains)
- Verify Recipe API returns consistent, realistic recipe counts
- Test sorting toggle functionality and persistence
- Manual testing of usage pattern calculations with mock historical data
- Edge case: Test sorting with items that have 0 recipes available
- Performance test: Verify sorting doesn't slow down list with 50+ items

**Post-Implementation Actions:**  
- Add custom sorting rules (user-defined priorities)
- Implement weighted scoring (combine all three criteria)
- Add sorting history/analytics dashboard
- Create sorting tips tooltip for new users

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Feature 3: Expiration Alerts & Visual Urgency Flags

**Purpose:**  
Notify users daily of items expiring within 3 days and provide visual urgency indicators (color-coded flags) so users immediately see which groceries need attention first.

**User Story / Use Case:**  
_As a user, I want to receive notifications when my groceries are expiring soon so that I can plan meals around them before they spoil, and I want to see at a glance which items are most urgent._

**Dependencies / Prerequisites:**  
- Add & Track Grocery Items feature (Feature 1)
- User authentication system
- Email/push notification service setup (SendGrid, Firebase Cloud Messaging)
- User notification preferences

**Technical Breakdown:**  
- **Frontend Components:**
  - `ExpirationFlag.tsx` (React + Tailwind CSS) – Color-coded visual indicator (green/yellow/red) on grocery cards with dynamic styling
  - `ExpirationAlertBanner.tsx` (React Toastify integration) – Prominent banner showing items expiring today/tomorrow with dismiss action
  - `NotificationSettings.tsx` (React Hook Form) – User preferences for alert frequency, delivery method, and quiet hours
  
- **Backend Endpoints (Node.js + Express):**
  - `GET /api/v1/groceries/expiring-soon?days=3` – Fetch items expiring within N days (cached)
  - `POST /api/v1/notifications/send-daily` – Scheduled job triggered by BullMQ (Cron: daily at user's preferred time); sends via Resend + Web Push
  - `PUT /api/v1/user/notification-preferences` – Update user alert settings (Zod validation)
  - `GET /api/v1/notifications/history` – Fetch notification log for user
  
- **Database Tables (Supabase PostgreSQL):**
  - `notifications` (id, user_id, item_id, notification_type, sent_at, delivered_at, read_at, delivery_method)
  - `user_notification_preferences` (user_id, enable_email_alerts, enable_push_alerts, alert_time, timezone, snooze_minutes, quiet_hours_start, quiet_hours_end)
  
- **Email & Push Services:**
  - **Resend** – Transactional email with React email templates; free tier: 100 emails/day
  - **Web Push API (Service Workers)** – Native browser push notifications; free, no third-party service needed
  
- **Key Logic:**
  - Calculate `days_until_expiration = estimated_expiration_date - today`
  - Red flag: `days_until_expiration <= 1`
  - Yellow flag: `1 < days_until_expiration <= 3`
  - Green flag: `days_until_expiration > 3`
  - BullMQ scheduled job runs daily; filters users by timezone; sends notifications respecting quiet hours and frequency preferences

**Implementation Steps:**  
- [ ] Step 1: Add color-coding logic to GroceryCard component
- [ ] Step 2: Create ExpirationFlag subcomponent (red/yellow/green)
- [ ] Step 3: Build ExpirationAlertBanner for dashboard
- [ ] Step 4: Implement backend expiring-soon endpoint
- [ ] Step 5: Set up email/push notification service (SendGrid, FCM)
- [ ] Step 6: Create scheduled notification job (cron/scheduler)
- [ ] Step 7: Build NotificationSettings UI component
- [ ] Step 8: Add user notification preferences to database
- [ ] Step 9: Implement notification history/log view
- [ ] Step 10: Test alert delivery and persistence
- [ ] Step 11: UI refinements (animations, sound for urgent items)

**Acceptance Criteria:**  
- [ ] Visual flags correctly color-code items by urgency (red/yellow/green)
- [ ] Daily notification sent for items expiring within 3 days
- [ ] Notifications arrive via email and/or push (per user preference)
- [ ] User can customize alert frequency and delivery method
- [ ] Alert banner appears on dashboard showing urgent items
- [ ] Notification can be dismissed or snoozed
- [ ] No duplicate notifications sent
- [ ] Alerts respect user timezone
- [ ] No console errors in notification flow
- [ ] Responsive alert UI on mobile

**Testing & Validation Notes:**  
- Create test items with expiration dates 0, 1, 2, 3, 4 days from today
- Verify correct flag colors appear for each expiration distance
- Test notification delivery via email and push
- Test user preference changes and verify notifications adjust accordingly
- Test snooze/dismiss functionality
- Timezone test: Verify alerts respect user's selected timezone
- Edge case: Test with 20+ items expiring on same day (no alert spam)

**Post-Implementation Actions:**  
- Add SMS alerts as option
- Create expiration alert history/analytics
- Build "save recipe for expiring item" quick action
- Add calendar view of upcoming expirations

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Feature 4: Recipe Suggestions Filtered by Expiring Items

**Purpose:**  
Display recipe recommendations prioritized by items expiring first, with ingredient availability indicators so users can see which recipes they can make with what they have.

**User Story / Use Case:**  
_As a cook, I want recipe suggestions based on the groceries I have that are about to expire so that I can use them before they spoil and discover meal ideas I might not have thought of._

**Dependencies / Prerequisites:**  
- Add & Track Grocery Items feature (Feature 1)
- Expiration Alerts feature (Feature 3)
- Recipe API integration (Spoonacular, Edamam, or similar)
- Backend user recipe history (optional: for personalized recommendations)

**Technical Breakdown:**  
- **Frontend Components:**
  - `RecipeSuggestions.tsx` (React + React Query) – Main container with infinite scroll and loading states
  - `RecipeCard.tsx` (Tailwind CSS + Framer Motion) – Recipe card with image, title, prep time, difficulty badge
  - `IngredientChecklistOverlay.tsx` (React Modal) – Full-screen modal showing required ingredients with ✓/⚠/✗ availability status
  - `RecipeFilters.tsx` (React Select + Tailwind) – Dropdowns for cuisine type, difficulty level, prep time range, dietary restrictions
  
- **Backend Endpoints (Node.js + Express):**
  - `GET /api/v1/recipes/by-expiring-items?limit=20&offset=0` – Get recipes sorted by expiring ingredient count (paginated)
  - `GET /api/v1/recipes/search?ingredient=chicken&cuisine=italian` – Search recipes via Spoonacular API with caching
  - `GET /api/v1/recipes/:recipeId/details` – Fetch full recipe (ingredients, instructions, nutrition from cache or API)
  - `POST /api/v1/user/saved-recipes` – Save/favorite recipe for user
  - `GET /api/v1/user/saved-recipes` – Fetch user's saved recipes
  
- **Database Tables (Supabase PostgreSQL):**
  - `saved_recipes` (id, user_id, recipe_id, recipe_name, api_source, image_url, saved_at, rating)
  - `recipe_cache` (recipe_id, recipe_name, ingredients, instructions, image_url, cuisine_type, prep_time_minutes, difficulty, nutrition, cached_at, expires_at)
  - Add index on `(user_id, saved_at DESC)` for fast retrieval of user's recipes
  
- **External APIs & Caching:**
  - **TheMealDB API** – Free, unlimited recipe search and ingredient matching (no authentication required)
  - **Upstash Redis** – Cache recipes and search results (48-hour TTL); free tier sufficient for MVP traffic
  
- **Key Logic:**
  - For each expiring item, query Spoonacular for recipes containing that ingredient
  - Calculate `expiring_ingredient_count` = number of user's expiring groceries in recipe ingredient list
  - Sort recipes by highest `expiring_ingredient_count` first, then by prep time
  - Match user's grocery quantities to recipe requirements; mark as ✓ (sufficient), ⚠ (limited/partial), ✗ (unavailable)
  - Apply user filters (cuisine, prep time, dietary restrictions) via query parameters

**Implementation Steps:**  
- [ ] Step 1: Integrate with Recipe API (Spoonacular or Edamam) and test queries
- [ ] Step 2: Build backend endpoint to fetch recipes by ingredient
- [ ] Step 3: Implement logic to match user's expiring items to recipe ingredients
- [ ] Step 4: Create RecipeCard component displaying recipe image, title, prep time
- [ ] Step 5: Build IngredientChecklistOverlay showing ingredient availability
- [ ] Step 6: Create RecipeSuggestions container with sorting/filtering
- [ ] Step 7: Add recipe filters (cuisine, difficulty, prep time, dietary)
- [ ] Step 8: Implement "save recipe" functionality
- [ ] Step 9: Build saved recipes view
- [ ] Step 10: Add recipe caching to reduce API calls
- [ ] Step 11: Unit tests for recipe matching algorithm
- [ ] Step 12: UI refinements (images, cards, animations)

**Acceptance Criteria:**  
- [ ] Recipe suggestions appear sorted by most expiring ingredients first
- [ ] Recipes display with image, title, prep time, and difficulty
- [ ] Ingredient availability indicators correctly show ✓/⚠/✗ status
- [ ] User can filter recipes by cuisine, prep time, dietary restrictions
- [ ] User can save/favorite recipes
- [ ] No console errors during recipe fetching/display
- [ ] Recipe API responses cached to reduce load times
- [ ] Responsive recipe card layout on mobile
- [ ] User can click recipe to view full ingredients and instructions
- [ ] "Cook this" action links to full recipe details

**Testing & Validation Notes:**  
- Test with grocery list containing 10 items (varied types: vegetables, proteins, dairy)
- Verify Recipe API returns relevant recipes containing at least 1 grocery item
- Test ingredient matching accuracy (fuzzy matching for "chicken" vs "chicken breast")
- Test recipe filtering by cuisine, prep time, dietary restrictions
- Test save/favorite functionality and persistence
- Performance test: Verify recipe loading doesn't exceed 2 seconds
- Edge case: Test with items that match very few recipes (e.g., niche ingredients)
- Mobile responsiveness testing (recipe cards, overlay modal, filters)

**Post-Implementation Actions:**  
- Add user ratings/reviews for recipes
- Implement "smart meal plans" (generate 3-day plans from expiring items)
- Add nutrition calculator to show macro/micronutrient info
- Create sharing functionality (share recipes with household members)
- Build recipe rating and favoriting analytics

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

## 🎯 Post-MVP Enhancements
> _Additional features, polish, and quality-of-life improvements planned after MVP deployment._

### Feature 5: Meal Planning & Weekly Meal Generator

**Purpose:**  
Generate balanced meal plans for the week using expiring groceries as the primary driver, helping users avoid waste while planning all their meals.

**User Story / Use Case:**  
_As a meal planner, I want the app to automatically suggest a weekly meal plan that prioritizes my expiring items so that I don't waste food and can plan my entire week efficiently._

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Feature 6: Shopping Predictions & Auto-Reorder

**Purpose:**  
Analyze user consumption patterns to predict when items will run out and suggest automatic reorders or shopping list additions.

**User Story / Use Case:**  
_As a frequent user, I want the app to learn my typical grocery usage and remind me to buy staples before I run out, so I never miss essential items._

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Feature 7: Multi-User Household Lists

**Purpose:**  
Enable family members or roommates to share a grocery list with role-based permissions (viewer, editor, admin).

**User Story / Use Case:**  
_As a parent, I want my family to see our shared grocery list and add items, so everyone knows what we have and can contribute to the inventory._

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Feature 8: Nutrition Analytics Dashboard

**Purpose:**  
Track macronutrients, calories, and dietary adherence across planned meals built from the grocery inventory.

**User Story / Use Case:**  
_As a health-conscious user, I want to see a summary of the nutrition in my meal plans so that I can ensure I'm eating balanced, healthy meals from my available groceries._

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

## 🎯 Experimental / Optional Features
> _Experimental or stretch features for exploration or testing._

### Feature 9: Barcode Scanning for Mobile

**Purpose:**  
Allow users to quickly add groceries by scanning product barcodes with their phone camera.

**User Story / Use Case:**  
_As a busy shopper, I want to scan barcodes at the store so that I can instantly add items to my list without typing._

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Feature 10: Grocery Store Price Comparison & Coupons

**Purpose:**  
Show price comparisons across local stores and highlight available coupons for items in the user's list.

**User Story / Use Case:**  
_As a budget-conscious shopper, I want to see which stores have the best prices for my groceries so that I can save money and plan my shopping trips efficiently._

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

## 🎯 Deployment & Integration Tasks
> _Steps for hosting, MCP setup, and production pipeline configuration._

### Deployment Task 1: Frontend Deployment (Vercel)

**Purpose:**  
Deploy React + Vite frontend to Vercel with automatic CI/CD from GitHub, environment management, and preview deployments.

**Tech Stack:**
- Vercel (hosting platform)
- GitHub Actions (CI/CD integration)
- Environment variables via Vercel dashboard

**Implementation Steps:**  
- [ ] Connect GitHub repository to Vercel project
- [ ] Configure environment variables (VITE_API_URL, VITE_SUPABASE_URL, VITE_SUPABASE_KEY, VITE_FCM_API_KEY)
- [ ] Set up automatic preview deployments for pull requests
- [ ] Configure custom domain and SSL (auto-renewed)
- [ ] Enable edge caching and optimize bundle size
- [ ] Set up error tracking (Sentry integration optional)

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Deployment Task 2: Backend Deployment (Railway)

**Purpose:**  
Deploy Node.js + Express backend to Railway with database connection pooling and automatic scaling.

**Tech Stack:**
- Railway (hosting platform for backend services)
- Node.js 20 LTS
- Environment variables via Railway dashboard

**Implementation Steps:**  
- [ ] Create Railway project and connect GitHub repository
- [ ] Configure environment variables (JWT_SECRET, DATABASE_URL, SENDGRID_API_KEY, SPOONACULAR_API_KEY, FCM_SERVICE_ACCOUNT_JSON, REDIS_URL)
- [ ] Set up automatic deployments from main branch
- [ ] Configure health check endpoint (`GET /api/v1/health`)
- [ ] Enable auto-scaling based on CPU/memory usage
- [ ] Configure error logging and monitoring (Sentry)
- [ ] Set up database connection pooling (PgBouncer)

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Deployment Task 3: Database Setup & Migrations (Supabase)

**Purpose:**  
Initialize Supabase PostgreSQL database with schema, Row-Level Security (RLS), and automated backups.

**Tech Stack:**
- Supabase (hosted PostgreSQL + auth + real-time - **Free tier**)
- Flyway (database migration tool - open source)
- pgAdmin (optional: database administration - open source)

**Implementation Steps:**  
- [ ] Create Supabase project (select region closest to users)
- [ ] Define database schema via migrations (users, groceries, item_types, notifications, saved_recipes, etc.)
- [ ] Implement Row-Level Security (RLS) policies (users can only view/edit their own data)
- [ ] Create database indexes for query performance (user_id, expiration_date, item_type)
- [ ] Set up automated daily backups (Supabase default: 7-day retention)
- [ ] Run migrations in staging environment before production
- [ ] Test replication and point-in-time recovery

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Deployment Task 4: Notification Services Setup (SendGrid + Firebase)

**Purpose:**  
Configure email (SendGrid) and push notification (Firebase Cloud Messaging) services with templates and error tracking.

**Tech Stack:**
- Resend (transactional email - **Free tier: 100 emails/day**)
- Web Push API (browser native push notifications - **Free, no service required**)
- BullMQ + Upstash Redis (job queue for scheduled notifications - **Free tier sufficient for MVP**)

**Implementation Steps:**  
- [ ] Create Resend account and configure domain for email authentication (SPF, DKIM)
- [ ] Design React email templates using Resend's React Email library (expiration alerts, welcome, password reset)
- [ ] Register Service Worker on frontend to handle push notifications
- [ ] Set up Upstash Redis queue with BullMQ for background job processing (free tier sufficient)
- [ ] Implement notification job: fetch users due for alerts, render React templates, send via Resend + Web Push
- [ ] Configure webhook endpoints to track email delivery status from Resend
- [ ] Test email delivery to multiple providers (Gmail, Outlook, Yahoo, etc.)
- [ ] Test push notification delivery on web browsers (Chrome, Firefox, Safari)
- [ ] Verify Resend free tier limits (100 emails/day) and implement optional email throttling for MVP

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

### Deployment Task 5: Recipe API & Caching Setup (Spoonacular + Redis)

**Purpose:**  
Integrate Spoonacular Recipe API with Redis caching layer to minimize API costs and improve response times.

**Tech Stack:**
- TheMealDB API (recipe data - **Free tier: unlimited requests, no authentication**)
- Upstash Redis (caching layer - **Free tier: 10,000 commands/day**)
- Node.js Redis client (redis library - open source)

**Implementation Steps:**  
- [ ] Integrate TheMealDB API (no registration needed; free tier unlimited requests)
- [ ] Design Upstash Redis cache structure (keys: `recipe:${id}`, `ingredient-recipes:${name}`, TTL: 48 hours)
- [ ] Implement API wrapper with error handling and cache check-before-fetch logic
- [ ] Monitor Upstash Redis usage (free tier: 10,000 commands/day sufficient for MVP; warn at 80%)
- [ ] Set up cache invalidation strategy (time-based TTL, manual refresh on user request)
- [ ] Test recipe search and details endpoints with TheMealDB mock data
- [ ] Load test with 100+ concurrent users to verify free tier performance
- [ ] Implement fallback behavior if TheMealDB is unavailable (serve stale cache from Redis)

**Status:** Not Started  
**Last Updated:** 2025-11-20

---

## 🎯 Development Notes
> _Chronological updates, milestones, or reflection logs (AI or developer-written)._

- **2025-11-20** – MVP Implementation Plan created with 4 core features: Add/Track Groceries, Smart Sorting, Expiration Alerts, Recipe Suggestions.
- **2025-11-20** – Feature dependencies mapped and technical breakdown documented for all MVP features.
- **2025-11-20** – Deployment tasks outlined for Vercel (frontend), Railway/Render (backend), Supabase (database), and third-party services.
- **2025-11-20** – Post-MVP enhancements identified: Meal Planning, Shopping Predictions, Multi-User Lists, Nutrition Analytics.
- **2025-11-20** – Experimental features brainstormed: Barcode Scanning, Store Price Comparison, Grocery Coupons.

---

## 📊 Feature Dependency Graph

```
Add & Track Groceries (Feature 1)
    ├─→ Smart Sorting (Feature 2)
    ├─→ Expiration Alerts (Feature 3)
    └─→ Recipe Suggestions (Feature 4)
            └─→ Meal Planning (Feature 5)
                    └─→ Nutrition Analytics (Feature 8)

Shopping Predictions (Feature 6) [depends on Feature 1]
Multi-User Lists (Feature 7) [depends on Feature 1]
Barcode Scanning (Feature 9) [depends on Feature 1]
```

**Recommended Implementation Order:**  
1. Feature 1 (Add & Track Groceries) – Foundation
2. Feature 3 (Expiration Alerts) – Core value prop
3. Feature 2 (Smart Sorting) – Enhances usability
4. Feature 4 (Recipe Suggestions) – Completes MVP
5. Deploy MVP to production
6. Feature 6 (Shopping Predictions) – Post-MVP
7. Feature 7 (Multi-User Lists) – Post-MVP
8. Feature 5 (Meal Planning) – Post-MVP
