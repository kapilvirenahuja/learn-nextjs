# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

### Development
- `pnpm dev` - Start development server with Turbopack for fast refresh
- `pnpm build` - Build for production
- `pnpm start` - Start production server

### Database
- Seed database: Make a GET request to `/app/seed/route.ts` endpoint
- Database queries: Available through functions in `/app/lib/data.ts`

## Architecture

This is a Next.js 15 dashboard application using the App Router architecture. It's part of the Next.js Learn Course and demonstrates modern patterns for building full-stack React applications.

### Key Architectural Decisions
- **App Router**: All routes are defined in `/app` directory using file-based routing
- **Server Components by Default**: Most components are React Server Components, with client components marked explicitly with `"use client"`
- **Data Access Layer**: All database operations are centralized in `/app/lib/data.ts` using raw SQL queries with the postgres client
- **Authentication**: Implemented using NextAuth v5 (beta) with credentials provider
- **Styling**: Tailwind CSS with custom design tokens defined in `tailwind.config.ts`

### Component Organization
- `/app/ui/dashboard/` - Dashboard-specific components (cards, charts, nav)
- `/app/ui/invoices/` - Invoice CRUD components with forms and tables
- `/app/ui/customers/` - Customer management components
- Shared components (buttons, search, skeletons) in `/app/ui/`

### Data Flow
1. Server Components fetch data directly using functions from `/app/lib/data.ts`
2. Forms use Server Actions for mutations
3. Client-side interactivity is limited to specific components marked with `"use client"`
4. Pagination and search are handled with URL search params

### Database Schema
- Users table for authentication
- Customers table for business entities
- Invoices table with status tracking (pending/paid)
- Revenue table for monthly financial data
- All models are typed in `/app/lib/definitions.ts`

## Development Notes

- This project uses `pnpm` as the package manager
- Turbopack is enabled for faster development builds
- Database operations require PostgreSQL connection
- Environment variables for database and auth must be configured
- Pagination is set to 6 items per page by default