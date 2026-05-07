# Stack Technique 2026

## Vue d'ensemble
Stack moderne, performante, et adaptée aux contraintes de sécurité et de scalabilité d'un SaaS financier.

| Couche | Technologie | Justification du CTO |
| :--- | :--- | :--- |
| **Front SaaS** | Next.js | SSR/SSG performant, standard de l'industrie. |
| **Marketing** | Astro | Vite, léger, SEO optimisé. |
| **Backend** | NestJS | Cadre strict (TS), injection de dépendances, parfait pour l'architecture modulaire et les règles métier complexes. |
| **Base de données**| PostgreSQL | ACID compliance absolue, essentielle pour la facturation et la comptabilité. |
| **ORM** | Prisma | Typage fort de bout en bout. *(Attention CTO : utiliser des types `Decimal` stricts, jamais de `Float` pour les devises).* |
| **Authentification**| Supabase | Sécurité robuste, RBAC natif, gain de temps sur le MVP. |
| **Stockage** | S3 compatible | Stockage pérenne et immuable des PDF et XML. |
| **Infrastructure** | AWS | Scalabilité, compliance, services managés. |
| **Edge / WAF** | Cloudflare | Protection DDoS, SSL natif, caching. |
| **Versionning** | GitHub | Standard. |
| **CI/CD** | GitHub Actions | Déploiement automatisé, linting, tests de sécurité. |
# Design Patterns & Standards

## Stack Cible (Source de Vérité)

| Couche | Tech |
| :--- | :--- |
| Front SaaS | Next.js |
| Marketing | Astro |
| API Métier | NestJS |
| DB | PostgreSQL |
| ORM | Prisma (`Decimal` obligatoire) |
| Auth | Supabase |
| Storage | S3 compatible |
| Infra | AWS |
| Edge / WAF | Cloudflare |
| Queue | Redis + BullMQ |
| Worker Documents | Python (Factur-X + PDF/A-3) |
| Génération PDF | Ghostscript |
| CI/CD | GitHub Actions |


## Pattern 1 : Gestion Financière (Immutabilité & Précision)
- **Règle** : Les entités financières (Factures) en statut "Finalisé" ou "Payé" sont **immuables**.
- **Tech** : Triggers PostgreSQL pour bloquer les `UPDATE` / `DELETE` sur ces enregistrements (Loi anti-fraude).
- **Précision** : Usage exclusif de `NUMERIC(18,4)` et `decimal.js`.

## Pattern 2 : Architecture du Monorepo
- **Outil** : NPM Workspaces ou Turborepo (à définir, focus simplicité).
- **Structure** :
  - `apps/web` (Next.js)
  - `apps/api` (NestJS)
  - `apps/worker` (Python)
  - `packages/database` (Prisma + types partagés)

## Pattern 3 : Asynchronisme Documentaire
- **Règle** : La génération Factur-X/PDF ne bloque **jamais** la requête HTTP utilisateur.
- **Workflow** : L'API NestJS répond un statut `202 Accepted` et un `job_id`. Le front poll (ou WebSockets) le statut du document généré par le Worker Python.

## Pattern 4 : Robustesse Worker (DLQ)
- **Dead Letter Queue** : Tout job Redis qui échoue (timeout Ghostscript, erreur XML) part en DLQ pour analyse manuelle sans paralyser la facturation globale.
