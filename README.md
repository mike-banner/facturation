# Facturation SaaS — Moteur de Conformité (API-First)

## 🎯 Vision du Projet
Plateforme B2B de facturation électronique conforme à la réforme 2026-2027 (Factur-X / EN16931). Ce projet n'est pas un simple logiciel de facturation, mais un **moteur de conformité robuste** exposé via une API publique pour permettre la verticalisation (BTP, Experts-comptables, E-commerce).

## 🛡️ Gouvernance (Staff Engineer Level)
Ce dépôt est régi par une règle stricte : **La documentation dirige le code.**
- Toute action de l'IA ou d'un développeur doit respecter les [RULES.md](docs/RULES.md).
- Aucune modification d'architecture sans une [ADR](docs/adr/) validée.
- **Dogme financier** : Zéro Float. Précision décimale absolue (`NUMERIC(18,4)` + `decimal.js`).

## 📂 Structure du Référentiel (Source of Truth)
La documentation centrale se trouve dans le dossier `/docs` :
- [MASTER_PLAN.md](docs/MASTER_PLAN.md) : Vision stratégique et monétisation.
- [ROADMAP.md](docs/ROADMAP.md) : État d'avancement et phases.
- [RULES.md](docs/RULES.md) : **Garde-fous immuables et standards.**
- [STACK.md](docs/STACK.md) : Technologies et patterns.
- [ARCHITECTURE.md](docs/ARCHITECTURE.md) : Flux de données et composants.
- [/docs/api](docs/api/) : Spécifications OpenAPI et contrats.
- [/docs/database](docs/database/) : Schémas, Tenancy et Audit-Log.

## 🚀 Stack Technique
- **Backend** : NestJS (TypeScript)
- **Frontend** : Next.js (SaaS) / Astro (Marketing)
- **Worker Documentaire** : Python (Factur-X / PDF/A-3 / Ghostscript)
- **Base de données** : PostgreSQL 16+ (Prisma ORM)
- **Infra** : AWS, S3, Redis (BullMQ), Cloudflare

---
*Projet en cours de développement — Phase 1 : Initialisation Technique.*
