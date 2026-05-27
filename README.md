# Taskly

A clean, minimal task management app
Focused on strong Next.js architecture over feature quantity.

![Next.js](https://img.shields.io/badge/Next.js-15.3-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-4-06B6D4?logo=tailwindcss)
![SQLite](https://img.shields.io/badge/SQLite-better--sqlite3-003B57?logo=sqlite)

---

## Features

- **Dashboard** — task list with stats cards and overall progress
- **Create Task** — form with title, description, due date, status, category
- **Task Detail** — shareable URL per task (`/tasks/123`)
- **Complete & Delete** — optimistic UI with instant feedback, no page reload
- **Collapsible Sidebar** — toggle between full and icon-only mode
- **Filter & Search** — filter by status, search by title
- **Error Handling** — `loading.tsx`, `error.tsx`, `not-found.tsx` at every route level

---

## Tech Stack

| Layer      | Technology                   |
| ---------- | ---------------------------- |
| Framework  | Next.js 15.3 (App Router)    |
| Language   | TypeScript 5                 |
| Styling    | Tailwind CSS v4              |
| Database   | SQLite via `better-sqlite3`  |
| Data Layer | Server Actions (no REST API) |
| UI Icons   | Lucide React                 |

---

## Project Structure

```
taskly/
├── app/
│   ├── layout.tsx                  # Root layout
│   ├── page.tsx                    # Redirects → /tasks
│   └── tasks/
│       ├── layout.tsx              # Sidebar shell
│       ├── page.tsx                # Dashboard (Server Component)
│       ├── loading.tsx             # Skeleton UI
│       ├── error.tsx               # Error boundary
│       ├── new/
│       │   └── page.tsx            # Create Task page
│       └── [id]/
│           ├── page.tsx            # Task Detail
│           ├── loading.tsx
│           ├── error.tsx
│           └── not-found.tsx
├── components/
│   ├── layout/
│   │   ├── Header.tsx
│   │   ├── Sidebar.tsx
│   │   └── SidebarLayout.tsx       # Toggle state lives here
│   └── tasks/
│       ├── TaskList.tsx            # Optimistic UI (complete/delete)
│       ├── TaskStatsCards.tsx
│       ├── TaskProgress.tsx
│       ├── CreateTaskForm.tsx
│       └── TaskDetailActions.tsx
└── lib/
    ├── db.ts                       # SQLite connection + auto-seed
    ├── queries.ts                  # Data access layer
    ├── actions.ts                  # Server Actions
    ├── types.ts                    # Shared TypeScript types
    └── utils.ts                    # Helpers, status/category configs
```

---

## Prerequisites

Make sure you have the following installed:

- **Node.js** `v22.x` (required for `better-sqlite3` native bindings)
- **npm** `v10+`

> ⚠️ If you're using a different Node version, `better-sqlite3` may fail to install with a version mismatch error. Use [nvm](https://github.com/nvm-sh/nvm) to switch:
>
> ```bash
> nvm install 22
> nvm use 22
> ```

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/AtanMegis/Taskly-Management-App.git
```

### 2. Install dependencies

```bash
npm install
```

If `better-sqlite3` fails with a native build error, rebuild it against your current Node version:

```bash
npm rebuild better-sqlite3
```

Or force a build from source:

```bash
npm install better-sqlite3 --build-from-source
```

### 3. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) — it redirects automatically to `/tasks`.

> The SQLite database is created automatically at `.data/taskly.db` on first run and seeded with sample tasks.

### 4. Build for production

```bash
npm run build
npm start
```

---

## Database

The app uses SQLite via `better-sqlite3`. No setup needed — the database file is created automatically.

**Location:**

```
.data/taskly.db
```

**To browse the database**, use one of:

- [DB Browser for SQLite](https://sqlitebrowser.org/) — open `.data/taskly.db` directly
- **VS Code extension** — search for "SQLite Viewer" by Florian Klampfer
- **CLI:**
  ```bash
  npx better-sqlite3-cli .data/taskly.db
  .tables
  SELECT * FROM tasks;
  ```

> The `.data/` folder is gitignored so your database stays local.

---

## Environment

No `.env` file is required. The app works out of the box with zero configuration.

---

## Scripts

| Command         | Description              |
| --------------- | ------------------------ |
| `npm run dev`   | Start development server |
| `npm run build` | Build for production     |
| `npm start`     | Start production server  |

---

## Troubleshooting

**`better-sqlite3` version mismatch error**

```
The module was compiled against a different Node.js version...
```

Fix:

```bash
npm rebuild better-sqlite3
# or
npm install better-sqlite3 --build-from-source
```

**Port already in use**

```bash
npm run dev -- -p 3001
```

**Database not seeding**
Delete the existing database file and restart:

```bash
rm .data/taskly.db
npm run dev
```

---

## License

MIT
