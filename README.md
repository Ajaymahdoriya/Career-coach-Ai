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
