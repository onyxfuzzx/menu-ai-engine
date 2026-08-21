# Menu AI Engine

Concise OCR + menu processing service with a .NET backend and a TypeScript frontend (Vite + Tailwind).

## Table of contents
- [Overview](#overview)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Local development](#local-development)
	- [Backend](#backend)
	- [Frontend](#frontend)
- [Database migrations](#database-migrations)
- [Testing](#testing)
- [Deployment notes](#deployment-notes)
- [Contributing](#contributing)
- [License](#license)

## Overview

This repository implements an OCR-driven menu ingestion and suggestion engine. It contains:

- `backend/` - ASP.NET Core Web API project (MenuOcrEngine) that handles OCR, normalization, menu suggestions, orders, sessions, and admin APIs.
- `frontend/` - Vite + TypeScript + Tailwind UI for admin/consumer interfaces and demo pages.

## Architecture

- The backend is a single .NET Web API project: `MenuOcrEngine.csproj`.
- Data layer uses Entity Framework Core (see `Data/AppDbContext.cs`).
- Migrations live under `Migrations/` and seed data under `Seed/`.
- The frontend is a modern SPA built with Vite (TypeScript) and TailwindCSS located in `frontend/`.

## Prerequisites

- .NET SDK (7.0+ recommended) — verify with `dotnet --version`.
- Node.js (16+ recommended) and npm or yarn for frontend tasks.
- A PostgreSQL or configured database as expected by the backend connection string (or use SQLite for quick local runs if configured).

## Local development

Follow these steps to run the backend and frontend locally.

### Backend

1. Open a terminal at the repo root and navigate to `backend/`:

```bash
cd backend
```

2. Restore and build the project:

```bash
dotnet restore
dotnet build
```

3. Configure appsettings: copy `appsettings.Example.json` to `appsettings.Development.json` and update the connection string and any keys.

4. Apply EF Core migrations (ensure your database is reachable):

```bash
dotnet ef database update
```

5. Run the API locally:

```bash
dotnet run
```

The API will listen on the configured URLs (check `appsettings.Development.json` and `Program.cs`). Controllers are available under `Controllers/` (examples: `MenuOcrController`, `OrdersController`, `SuggestorController`).

### Frontend

1. Change into the frontend folder and install dependencies:

```bash
cd frontend
npm install
# or: yarn
```

2. Run the dev server:

```bash
npm run dev
```

3. Build for production:

```bash
npm run build
```

The Vite dev server serves the UI; configuration lives in `vite.config.ts` and `src/` contains the application source.

## Database migrations

Migrations are managed with EF Core and are located in `backend/Migrations/`.

To add a new migration from `backend/`:

```bash
cd backend
dotnet ef migrations add <MigrationName>
dotnet ef database update
```

## Testing

If/when tests are added, run them from the `backend/` project with:

```bash
dotnet test
```

Frontend tests (if present) can be run via the configured test runner in `frontend/` (e.g., `npm test`).

## Deployment notes

- Ensure production `appsettings.json` contains production-ready connection strings and secrets; prefer environment variables or a secrets store.
- Build the frontend and serve the static assets from a CDN or behind the API as desired.
- Use standard .NET deployment practices (containers, Azure App Service, or other hosts).

## Contributing

Contributions are welcome. Please open issues or PRs describing the change. Follow these guidelines:

- Create a branch per feature/bugfix.
- Keep changes focused and add tests where appropriate.
- Run migrations and include migration files if schema changes are required.

## License

Specify your license here (e.g., MIT). If you have a `LICENSE` file, reference it.

---

If you'd like this README to include more detailed developer workflows, API examples, or environment variable references, tell me which sections to expand.


