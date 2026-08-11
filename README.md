# My Little Warehouse (MLW)

A multi-user inventory management web app built for small businesses to track items, photos, and status across a shared warehouse — built from scratch with vanilla HTML/CSS/JS and Supabase.

Originally built to solve a real problem: managing furniture/inventory across moving and staging jobs, where multiple people need to see and update the same inventory without stepping on each other's data.

## Features

- **Multi-user authentication** — full auth flow including sign-up, sign-in, email confirmation, and forgot/reset password, each with dedicated screens
- **Row-Level Security (RLS)** — every user only sees and modifies their own inventory data, enforced at the database level, not just in the UI
- **Inventory CRUD** — add, edit, and delete items, including photo upload to Supabase Storage
- **Grid & list views** — toggle between a visual grid and a compact list depending on how much detail you need
- **Search & filtering** — client-side search across title, description, category, and location, plus filters by status, condition, and category
- **Responsive item cards** — image-forward cards with an overlay menu for quick edit/delete actions

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript (no framework) |
| Backend | [Supabase](https://supabase.com) — Postgres database, Auth, Storage |
| Hosting | Static hosting via SFTP |

## Architecture Notes

- **Database**: a single `Items` table (`id`, `user_id`, `title`, `description`, `category`, `condition`, `status`, `location`, `listing`, `images`) with `user_id` as a foreign key used to scope every RLS policy
- **Auth**: Supabase Auth handles sessions; every read/write goes through RLS policies keyed to the authenticated user, so access control lives in the database, not just in client-side checks
- **Storage**: item photos are uploaded to a dedicated Supabase Storage bucket and referenced by URL in the `images` field
- **No framework, intentionally** — built in vanilla JS to focus on understanding the full request/response and auth lifecycle without abstraction

## Why I built this

I run a small moving and staging labor business (Covele Deeds) and kept seeing the same problem on jobs: inventory tracked in text threads and spreadsheets that nobody trusted. MLW was my attempt to build a real tool for that — and to learn full-stack development, auth, and database security by building something with an actual user in mind rather than a tutorial project. I piloted it with two local businesses to get real feedback on the workflow.

## Status

Actively developed as a personal/portfolio project. Planned next steps include analytics/dashboard views, CSV export, and mobile responsiveness improvements.

