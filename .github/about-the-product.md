# About the Product – Roy's Meal Assistant: Grocery List Companion

This document defines the product vision, audience, purpose, and evolving direction of the application.  
It provides **contextual memory** for the AI to ensure all code and features align with the product's goals and identity.

---

## 🤖 AI Interaction Rules

1. **Always review this document before implementing, refactoring, or suggesting new features.**  
   Use this file to align development choices with the product's intent, tone, and audience.

2. **When updating or refining product details:**
   - Edit only the relevant sections (Purpose, Target Audience, etc.).  
   - Maintain the existing Markdown heading structure.  
   - Avoid removing historical context unless it's outdated or replaced with updated data.  
   - When a major change occurs (like a new direction or rebrand), summarize it in the "Product Evolution Log."

3. **When adding new information:**
   - Place it under the correct section heading.  
   - Use clear, concise, human-readable language.  
   - Maintain professional tone and formatting consistency.

4. **Do not change section titles or structure.**
   - Keep this format intact so the AI can reliably read and update fields.

5. **Use dates for all updates.**
   - Include timestamps in "Product Evolution Log" whenever meaningful updates occur.

---

## 📋 Product Information

---

## 🎯 Product Name

**Roy's Meal Assistant: Grocery List Companion**

---

## 🎯 Purpose / Mission

Roy's Meal Assistant solves the critical problem of **food waste and meal planning inefficiency**. Users struggle to remember what groceries they have at home, when items will expire, and what meals they can prepare with available ingredients. This app bridges that gap by providing intelligent grocery tracking with automatic expiration date estimation, visual urgency alerts, and smart recipe discovery—enabling users to use their groceries before they spoil and discover meal ideas from what they already own.

---

## 🎯 Target Audience

- **Home cooks and meal planners** (ages 25-55) who want to reduce food waste and plan meals efficiently
- **Budget-conscious households** looking to optimize grocery spending and minimize waste
- **Busy professionals** who need quick, simple tools to track groceries without friction
- **Environmentally-minded consumers** concerned about sustainability and reducing household waste

---

## 🎯 Core Value Proposition

Roy's Meal Assistant is unique because it combines three powerful capabilities in one simple tool:
1. **Automatic expiration tracking** – No manual entry; the system intelligently estimates expiration dates based on item type
2. **Smart ingredient sorting** – Lists ingredients by versatility (number of recipes), quantity on hand, and forecasted needs
3. **Expiration-driven recipe discovery** – Users see recipe suggestions tailored to items expiring first, reducing waste while sparking meal ideas

**Result:** Users consume 80% of groceries before expiration, save time planning meals, and reduce household food waste.

---

## 🎯 MVP Objective

The MVP launches with four core features:

1. **Add & Track Grocery Items with Auto-Expiration** – Users add items; the system auto-estimates expiration dates based on item type (e.g., milk: 7 days, eggs: 30 days, bread: 5 days)
2. **Smart Grocery List Sorting** – Items ranked by number of recipe uses (versatility), quantity on hand, and forecasted purchase needs
3. **Expiration Alerts** – Daily notifications for items expiring within 3 days; visual urgency flags (red for expiring today/tomorrow)
4. **Recipe Suggestions** – Single-click recipe recommendations filtered to items expiring first, with ingredient availability indicators

Success is measured by: **80% of users consuming added groceries before expiration within the first month of use.**

---

## 🎯 Long-Term Vision

**Phase 2 (Post-MVP):**
- **Meal Planning Integration** – Generate weekly meal plans from expiring ingredients
- **Shopping Predictions** – AI forecasts future grocery needs based on usage patterns
- **Nutrition Analytics** – Track macros, calories, and dietary goals across planned meals
- **Community Recipes** – Browse user-submitted recipes filtered by dietary preferences and available ingredients
- **Grocery Store Integration** – Link to store coupons and price comparisons for items in the list
- **Multi-user Household Lists** – Shared grocery lists for families with role-based permissions

**Vision (3+ years):**
- Mobile app with barcode scanning for instant item addition
- Integration with grocery delivery services (Amazon Fresh, Instacart)
- AI meal planning with dietary restrictions and allergy management
- Smart fridge camera recognition
- Sustainability dashboard tracking personal food waste reduction

---

## 🎯 Design & Experience Principles

- **Simplicity First** – Minimal clicks to add items; auto-filled fields reduce user input friction
- **Visual Urgency Hierarchy** – Red flags for expiring items make priorities immediately clear
- **Progressive Disclosure** – Basic functionality on first visit; advanced sorting and analytics appear as users explore
- **Accessibility & Responsiveness** – Works seamlessly on mobile, tablet, and desktop; WCAG 2.1 AA compliant
- **Warm, Encouraging Tone** – Language celebrates waste reduction and smart meal choices rather than scolding
- **Consistent Icons & Colors** – Green for fresh items, yellow for medium urgency, red for expiring soon

---

## 🎯 Technical Overview

**Frontend:**
- React 18+ with TypeScript
- Vite for fast build and development
- Tailwind CSS for responsive design
- React Query for state management and caching
- Notifications library (e.g., React Toastify) for alerts

**Backend:**
- Node.js + Express.js or Python + Flask
- REST API with JWT authentication
- Database: Supabase (PostgreSQL) for scalability and real-time features

**Additional Services:**
- Authentication: Clerk or Supabase Auth
- Notifications: SendGrid (email) + push notification service (Firebase Cloud Messaging)
- Hosting: Vercel (frontend), Railway or Render (backend)

**Key Integrations:**
- Recipe API (Spoonacular, Edamam, or similar) for recipe suggestions
- Mobile push notifications for expiration alerts

---

## 🎯 Product Structure Overview

The app is organized into **5 main sections:**

1. **Dashboard/Home** – At-a-glance view of grocery inventory, expiring items, and quick-add button
2. **Grocery Inventory** – Full list of all items sorted by versatility, quantity, and expiration urgency
3. **Expiration Alerts** – Dedicated view for items expiring within 3 days with notification settings
4. **Recipe Discovery** – Filterable recipe cards tied to expiring ingredients; ingredient checklist overlay
5. **Settings & Profile** – User preferences, notification frequency, dietary restrictions, and account management

---

## 🎯 Product Evolution Log

- **2025-11-20** – Initial product concept defined: Grocery List Assistant focused on reducing food waste through smart expiration tracking and recipe discovery.
- **2025-11-20** – Core MVP features established: Add/track groceries, auto-expiration, smart sorting (versatility/quantity/forecasted needs), expiration alerts, recipe suggestions.
- **2025-11-20** – Success metric defined: 80% of users consuming groceries before expiration within first month.
- **2025-11-20** – Technical stack outlined: React + Express/Flask + Supabase + Recipe API integrations.

---

## 🎯 File Integrity Notes

- Preserve Markdown headings and section order.  
- Keep whitespace between sections.  
- Avoid embedding raw code here – this file is conceptual, not technical.  
- AI should write clear, concise, descriptive English.  
- Always timestamp meaningful updates.
