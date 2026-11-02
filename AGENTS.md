# Repository guidance

This repository is a Clean Architecture Blazor Server solution. See `README.md` for setup and `docs/` for project documentation.

## Project structure

- `src/Domain`: entities, domain events, and business rules. Keep this layer independent of UI and infrastructure.
- `src/Application`: use cases, DTOs, validators, specifications, and service contracts. Feature code lives in `src/Application/Features`.
- `src/Infrastructure`: persistence, authentication, caching, background jobs, and external integrations.
- `src/Server.UI`: the Blazor Server host, pages, components, and UI services.
- `src/Migrators`: EF Core migration projects for SQL Server, PostgreSQL, and SQLite.
- `tests/`: application, domain, and infrastructure test projects.
- `docs/superpowers/`: design notes, plans, and implementation specifications when needed.

## Working in this repository

- Keep changes focused and follow nearby project patterns. Do not refactor unrelated code.
- Preserve Clean Architecture boundaries. Before adding a feature, inspect similar code in `Application`, `Infrastructure`, and `Server.UI`.
- Update documentation when setup steps, commands, or workflows change.
- Explain assumptions when behavior is unclear. Keep changes small and reviewable.
- Run the narrowest meaningful verification. Report when verification could not be performed.

## Common commands

Build and test the solution:

```bash
dotnet build CleanArchitecture.Blazor.slnx
dotnet test CleanArchitecture.Blazor.slnx
```

Run the Blazor Server app:

```bash
dotnet run --project src/Server.UI
```

Create a SQL Server migration. Replace `<MigrationName>` with a new name:

```bash
dotnet ef migrations add <MigrationName> --project src/Migrators/Migrators.MSSQL --startup-project src/Server.UI --context ApplicationDbContext --output-dir Migrations
```

Apply SQL Server migrations:

```bash
dotnet ef database update --project src/Migrators/Migrators.MSSQL --startup-project src/Server.UI --context ApplicationDbContext
```
