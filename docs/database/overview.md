# Database Overview

## Infrastructure
- **Engine**: PostgreSQL 16+
- **Host**: AWS RDS (Production) / Docker (Local)
- **ORM**: Prisma (TypeScript)

## Naming Standards
- **Tables**: Plural, `snake_case` (ex: `invoice_lines`).
- **Columns**: `snake_case` (ex: `created_at`).
- **Primary Keys**: Always `id` as `UUID v4`.
- **Foreign Keys**: `entity_id` (ex: `company_id`).

## Data Integrity
- **Money**: `NUMERIC(18,4)`.
- **Dates**: `TIMESTAMP WITH TIME ZONE` (TIMESTAMPTZ).
- **Audit**: Every table must have `created_at` and `updated_at`.
