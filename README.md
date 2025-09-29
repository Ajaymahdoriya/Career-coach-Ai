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
