# NESTOOD

**Built around how you live.**

A construction website for exploring homes, commercial spaces, renovations, and interiors. NESTOOD brings together a project portfolio, service information, package comparisons, and an interactive cost calculator, with content focused on Chennai and Bengaluru.

[Live website](https://nestood-construction-website--rahulsangral.replit.app/) | [GitHub repository](https://github.com/sangralrahul/NESTOOD)

## Features

- Responsive layouts, mobile navigation, architectural visuals, and motion effects with reduced-motion support.
- Service descriptions, company information, and Basic, Standard, and Premium construction packages.
- Project listings filtered by category, status, and location, with individual project pages.
- Location information, a testimonial carousel, searchable FAQs, and a journal with category filters and article pages.
- Cost estimates using built-up area, construction type, location adjustments, floor adjustments, and optional allowances.
- Contact and estimate forms that save enquiries in the current browser.
- An admin interface for reviewing enquiries, updating statuses, assigning leads, recording notes and follow-up dates, editing content, and adjusting calculator rates.

## Pages

| Area | Routes |
| --- | --- |
| Home and company | `/`, `/about` |
| Services and pricing | `/services`, `/packages` |
| Project portfolio | `/projects`, `/projects/:slug` |
| Locations and reviews | `/locations`, `/testimonials` |
| FAQs and journal | `/faq`, `/blog`, `/blog/:slug` |
| Enquiries and estimates | `/contact`, `/calculator` |
| Admin dashboard and leads | `/admin`, `/admin/leads` |
| Content management | `/admin/projects`, `/admin/packages`, `/admin/services`, `/admin/testimonials`, `/admin/locations`, `/admin/blog` |
| Calculator settings | `/admin/calculator` |

## Technology

The frontend uses **React 19**, **TypeScript**, **Vite 7**, and **Tailwind CSS 4**. Wouter handles routing; Framer Motion provides animations; Lucide and Radix-based UI components support the interface. The design uses DM Sans and Instrument Serif with navy, teal, and ivory colours.

The pnpm workspace also contains an Express API scaffold, an OpenAPI specification, generated API clients and validators, and a Drizzle/PostgreSQL database scaffold.

## Run locally

Install Git and Node.js 24, which includes npm. These commands use pnpm 10 through `npx`; a global pnpm installation is not required.

Run in Windows CMD:

```bat
git clone https://github.com/sangralrahul/NESTOOD.git
cd NESTOOD
npx --yes pnpm@10 install --frozen-lockfile
npx --yes pnpm@10 --filter @workspace/nestood-site run dev
```

Open [http://localhost:5173](http://localhost:5173). The admin interface is at [http://localhost:5173/admin](http://localhost:5173/admin).

The current frontend runs without a database or API server. Vite defaults to port `5173` unless `PORT` is set.

## Build and preview

From the repository root, build the workspace, including its TypeScript checks:

```bat
npx --yes pnpm@10 run build
```

The website output is written to `artifacts/nestood-site/dist/public`.

Stop the development server before previewing on the same port:

```bat
npx --yes pnpm@10 --filter @workspace/nestood-site run serve
```

For static hosting, publish that output directory and configure a fallback to `index.html` for client-side routes such as `/projects` and `/contact`.

## Project structure

| Path | Purpose |
| --- | --- |
| `artifacts/nestood-site/` | Public website and admin interface |
| `artifacts/api-server/` | Express API scaffold |
| `artifacts/mockup-sandbox/` | Separate component preview workspace |
| `lib/api-spec/` | OpenAPI specification and generation configuration |
| `lib/api-client-react/`, `lib/api-zod/` | Generated API client and validation code |
| `lib/db/` | Database connection and schema scaffold |
| `attached_assets/` | Bundled project assets |
| `scripts/` | Workspace utility scripts |

Most website pages, initial content, and admin logic are in `artifacts/nestood-site/src/App.tsx`. Shared styling is in `artifacts/nestood-site/src/index.css`.

## Current implementation

- **Browser-local data:** enquiries, admin content, and calculator settings use `localStorage`. They are not shared between browsers or devices, and clearing site data removes them. Form submission does not send an email or save to a server.
- **Admin access:** admin routes currently have no authentication or role checks.
- **Starter content:** the project includes seeded content and placeholder media. Some homepage sections and the package comparison table use fixed values rather than admin-edited records.
- **Calculator behaviour:** configured construction-type rates determine the base price. The selected package rate is only a fallback when a type has no configured rate. Estimates are indicative and exclude land, taxes, and statutory fees.
- **Backend scope:** the API currently exposes `GET /api/healthz`. The database and generated API packages are not connected to the enquiry or content workflows.

## Maintainer

[Rahul Sangral](https://github.com/sangralrahul)
