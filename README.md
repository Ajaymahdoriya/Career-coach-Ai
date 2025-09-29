# AI Career Coach — README

A full-stack Next.js application that helps professionals accelerate their careers with AI-powered tools: industry insights, resume building, cover letter generation, and interview preparation. It uses Clerk for auth, Prisma + PostgreSQL for data, Google Generative AI (Gemini) for content generation, and Inngest for scheduled background updates.

## Features

- Authentication and user management with Clerk
- Onboarding with industry and skills to personalize insights
- AI Industry Insights dashboard with:
    - Growth rate, demand level, market outlook
    - Salary ranges by role (chart)
    - Top skills, key trends, and recommended skills
- AI Resume Builder
    - Structured form → Markdown resume
    - “Improve with AI” for bullet points
    - Live Markdown preview and PDF export
    - Save resume to DB
- AI Cover Letter Generator
    - Tailored to job title, company, user profile, and JD
    - Markdown output and persistent storage
- AI Interview Preparation
    - 10-question MCQ quizzes based on industry/skills
    - Explanations, scoring, analytics, improvement tip
    - History, stats cards, performance trend
- Weekly auto-refresh of industry insights via Inngest cron

## Tech Stack

- Framework: Next.js (App Router), React, Server Actions
- UI: Tailwind CSS, shadcn/radix primitives, Recharts, @uiw/react-md-editor, Sonner
- Auth: Clerk
- AI: Google Generative AI (Gemini 1.5 Flash)
- DB/ORM: PostgreSQL + Prisma
- Scheduler: Inngest
- Misc: date-fns, html2pdf.js

## Project Structure

- actions/ — Server actions for cover letters, dashboard insights, interview, resume, and user profile
- app/ — App Router pages and routes (auth, main sections, API, lib)
    - (auth)/ — Sign-in/up (Clerk)
    - (main)/ — Dashboard, Resume, Cover Letters, Interview, Onboarding
    - api/inngest/route.js — Inngest handler
    - lib/ — app-level helpers and schemas for forms
- components/ — UI primitives and shared components (Header, ThemeProvider)
- data/ — Static site content for the landing page
- hooks/ — Custom hooks (useFetch)
- lib/ — Prisma client, utils, Clerk user bootstrap, Inngest client/functions
- prisma/ — Prisma schema and SQL migrations
- public/ — Static assets (banner images)
- Configs — Next, Tailwind, ESLint, PostCSS

## Prerequisites

- Node.js 18+
- PostgreSQL database
- API keys and secrets:
    - CLERK_SECRET_KEY, NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY
    - DATABASE_URL (PostgreSQL)
    - GEMINI_API_KEY (Google Generative AI)
    - INNGEST signing (optional for local; needed for production)
 
## Environment Variables

Create a .env.local file:

- DATABASE_URL=postgres://USER:PASSWORD@HOST:PORT/DB
- NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_xxx
- CLERK_SECRET_KEY=sk_test_xxx
- GEMINI_API_KEY=your_gemini_api_key
- (Optional) Inngest related variables depending on deployment


## Installation

1) Install dependencies

- npm install

2) Generate Prisma client

- npx prisma generate

3) Run migrations

- npx prisma migrate deploy
- Or for development:
    - npx prisma migrate dev

4) Start the dev server

- npm run dev

## Database

- Prisma models: User, Assessment, Resume, CoverLetter, IndustryInsight
- Users are auto-created from Clerk on first request (lib/checkUser.js)
- One Resume per user (unique userId)
- IndustryInsight is referenced by User.industry (optional relationship)

Run Prisma Studio for quick inspection:

- npx prisma studio


## Authentication

- Clerk is initialized in app/layout.js via ClerkProvider
- Sign-in/up routes under app/(auth)
- SignedIn/SignedOut components used in the Header

## AI Integrations

- Google Generative AI (Gemini 1.5 Flash)
    - actions/cover-letter.js: generateCoverLetter
    - actions/interview.js: generateQuiz + improvement tips
    - actions/resume.js: improveWithAI for descriptions
    - actions/dashboard.js + lib/inngest/function.js: industry insights JSON

Note: Ensure GEMINI_API_KEY is set and billing/quota allows usage.

## Background Jobs (Inngest)

- Cron “Generate Industry Insights” runs weekly (Sunday midnight) to refresh insights
- Handler: app/api/inngest/route.js
- Function: lib/inngest/function.js
