# Roadmap & Plan d'Exécution

## RÈGLE D'ARCHIVAGE
> Quand une phase passe à `[x]` : créer un fichier dans `.memory/history/YYYY-MM-DD_phaseN_nom.md` avec la date, les points réalisés et les décisions prises.

---

## VISION : MOTEUR DE CONFORMITÉ FISCALE (API-FIRST)
```
COUCHE 3 — VERTICAL SAAS (produits marchands)
   BTP / Experts-Comptables / E-commerce

COUCHE 2 — API PUBLIQUE (vecteur de revenus #1)
   API Factur-X · API Conformité · SDK · Webhooks

COUCHE 1 — MOTEUR CONFORMITÉ (ce qu'on build d'abord)
   XML EN16931 · PDF/A-3 · Validation · PAF · E-Reporting
```

---

## GLOBAL OVERVIEW — TABLEAU DE BORD

| Phase | Titre | Deadline | Statut |
| :---: | :--- | :--- | :---: |
| **0** | Stratégie, Mémoire & Vision | ✅ 07/05/2026 | ✅ Terminée |
| **1** | Monorepo, DB & Infrastructure | — | 🔄 En cours |
| **2** | Moteur Conformité (Cœur) | **Avant Sept. 2026** | `[ ]` |
| **3** | API Publique & Auth Développeur | **Avant Sept. 2026** | `[ ]` |
| **4** | SaaS Wrapper (Dashboard, Auth, Billing) | Q4 2026 | `[ ]` |
| **5** | White-label Experts-Comptables | Q4 2026 | `[ ]` |
| **6** | Intégration PDP / PPF & E-Reporting | **Sept. 2026 / Sept. 2027** | `[ ]` |
| **7** | Vertical SaaS #1 (BTP ou E-commerce) | 2027 | `[ ]` |
| **8** | Sécurité, Tests & Observabilité | Continu | `[ ]` |
| **9** | OCR, IA & Automatisation | Post-MVP | `[ ]` |

---

## PHASE 0 : STRATÉGIE & STRUCTURE `[x]`
> **Archivé le 07/05/2026** → `.memory/history/2026-05-07_phase0_setup.md`

- [x] Initialisation mémoire (`.memory/`)
- [x] Vision réorientée : Moteur de conformité API-First
- [x] Stack Technique validée
- [x] Règles Comptables strictes (Decimal / Anti-Float)
- [x] Stratégie Documentaire (Worker Python + Ghostscript)
- [x] Compliance France / EU documentée
- [x] Stratégie de monétisation (API + Verticals)
- [x] System Prompts IA (`claude.md`, `antigravity.md`)
- [x] Design Patterns & dossier `.memory/adr/` (ADR-001, 002, 003)
- [x] Création du fichier `RULES.md` à la racine
- [x] Registre History opérationnel

---

## PHASE 1 : MONOREPO & BASE DE DONNÉES `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase1_monorepo.md`

### 1.1 Setup Monorepo (Turborepo)
- [ ] Init Turborepo + `package.json` root
- [ ] Scaffold `apps/api` (NestJS)
- [ ] Scaffold `apps/web` (Next.js — Dashboard SaaS)
- [ ] Scaffold `apps/marketing` (Astro)
- [ ] Scaffold `apps/worker` (Python / Poetry — Moteur Document)
- [ ] Scaffold `packages/database` (Prisma + types)
- [ ] Scaffold `packages/types` (Types TS partagés inter-apps)
- [ ] Scaffold `packages/config` (ESLint, TS, Prettier)

### 1.2 Infrastructure Locale
- [ ] `docker-compose.yml` : PostgreSQL + Redis + PgAdmin
- [ ] `.env.example` documenté (toutes les variables)
- [ ] `Makefile` pour commandes courantes (dev, migrate, test, worker)

### 1.3 Modélisation Base de Données (Prisma)
- [ ] Modèle `Organization` (Multi-tenant root — SIREN, TVA, Config)
- [ ] Modèle `ApiKey` (Pour l'API Publique — Phase 3)
- [ ] Modèle `Client`
- [ ] Modèle `Product` / `Service` (Prix HT `Decimal`, Taux TVA)
- [ ] Modèle `Invoice` (Statut, Numérotation séquentielle)
- [ ] Modèle `InvoiceLine` (Tous champs monétaires `Decimal`)
- [ ] Modèle `AuditLog` (Immuable — PAF obligatoire)
- [ ] Modèle `DocumentJob` (Suivi async des générations PDF/XML)
- [ ] Modèle `EReportingEntry` (Pour la transmission DGFiP — Phase 6)
- [ ] Triggers SQL : Immutabilité des factures finalisées
- [ ] Politique rétention S3 : 10 ans (obligation légale)
- [ ] Première migration

### 1.4 Dogme Decimal
- [ ] `decimal.js` configuré dans `apps/api`
- [ ] Helper `money.ts` (add / multiply / round / format)
- [ ] Tests unitaires d'arrondi

---

## PHASE 2 : MOTEUR DE CONFORMITÉ (CŒUR DU PRODUIT) `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase2_moteur.md`
> ⚠️ **DEADLINE : Avant le 1er septembre 2026**

### 2.1 Queue & Worker Python
- [ ] Setup BullMQ (Redis) dans `apps/api`
- [ ] Producer NestJS → Job `generate-document`
- [ ] Consumer Python → Dépile et génère
- [ ] DLQ (Dead Letter Queue) : Jobs en échec isolés
- [ ] Suivi statut dans `DocumentJob` (DB)

### 2.2 Génération XML EN16931 (Worker Python)
- [ ] Sélection librairie Python (`factur-x`, `drafthorse` ou autre)
- [ ] Génération XML CII complet selon EN16931
- [ ] Injection de TOUS les champs obligatoires DGFiP :
  - [ ] SIREN / SIRET émetteur
  - [ ] N° TVA intracommunautaire
  - [ ] Numéro de facture (séquentiel non réutilisable)
  - [ ] Date émission + Date prestation/livraison
  - [ ] Identité complète client
  - [ ] Lignes détaillées (HT + Taux TVA + Montant TVA)
  - [ ] Totaux HT / TVA / TTC
  - [ ] Conditions de règlement (délai, mode, pénalités)
- [ ] Validation XML contre schéma XSD officiel EN16931
- [ ] Tests de conformité automatisés

### 2.3 Génération PDF/A-3
- [ ] Template HTML facture (Jinja2 + WeasyPrint ou équivalent)
- [ ] Conversion PDF/A-3 via Ghostscript
- [ ] Embedding XML EN16931 dans le PDF/A-3 (Factur-X hybride)
- [ ] Validation PDF/A-3 (VeraPDF)
- [ ] Tests de lecture par logiciels tiers (vérification embedding)

### 2.4 Archivage & PAF
- [ ] Upload S3 (chemin immuable + versionning activé)
- [ ] `AuditLog` écrit à chaque changement de statut
- [ ] Politique de rétention S3 configurée (10 ans)

### 2.5 Cas TVA Spéciaux
- [ ] TVA standard : 20%, 10%, 5.5%, 2.1%
- [ ] Franchise en base (mention "TVA non applicable")
- [ ] TVA intracommunautaire (mention "Autoliquidation")
- [ ] Export hors UE (mention "Exonéré de TVA")

---

## PHASE 3 : API PUBLIQUE & PORTAIL DÉVELOPPEUR `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase3_api.md`
> ⚠️ **DEADLINE : Avant le 1er septembre 2026 (Réforme)**

### 3.1 API Layer NestJS
- [ ] Gestion des `ApiKey` (génération, révocation, scopes)
- [ ] Rate limiting par clé API (tier Free / Pro / Enterprise)
- [ ] Versioning API (`/v1/`)
- [ ] Réponses standardisées (erreurs, codes HTTP)

### 3.2 Endpoints Publics du Moteur
- [ ] `POST /v1/invoices` → Création et génération Factur-X
- [ ] `GET /v1/invoices/:id` → Récupération statut + liens
- [ ] `POST /v1/validate` → Validation d'un XML EN16931 externe
- [ ] `GET /v1/documents/:id/pdf` → Téléchargement PDF/A-3
- [ ] `GET /v1/documents/:id/xml` → Téléchargement XML CII

### 3.3 Documentation & Sandbox
- [ ] Documentation OpenAPI (Swagger auto-généré par NestJS)
- [ ] Sandbox (Environnement de test isolé avec données fictives)
- [ ] SDK JavaScript (Wrapping de l'API en client typé)
- [ ] Guide de démarrage rapide (README + exemples Postman)

---

## PHASE 4 : SAAS WRAPPER (DASHBOARD, AUTH, BILLING) `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase4_saas.md`

- [ ] Supabase Auth (Magic Link + OAuth)
- [ ] RBAC : Rôles `owner`, `admin`, `accountant`, `viewer`
- [ ] Onboarding (Setup guidé SIREN, TVA, Logo, Coordonnées)
- [ ] Dashboard (CA mensuel, factures en attente, statuts)
- [ ] Intégration Stripe (Abonnements + Pay-as-you-go)
- [ ] Webhooks Stripe (activation/désactivation compte)
- [ ] Envoi factures par email (Resend / SendGrid)
- [ ] Portail client (Vue publique partageable)

---

## PHASE 5 : WHITE-LABEL EXPERTS-COMPTABLES `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase5_whitelabel.md`

- [ ] Mode multi-clients par cabinet (1 cabinet → N clients PME)
- [ ] Branding personnalisable (Logo, Couleurs, Domaine)
- [ ] Interface de gestion de portefeuille clients
- [ ] Export pour logiciels comptables (Cegid, Sage — format spécifique)
- [ ] Tableau de bord cabinet (vue consolidée tous clients)
- [ ] Plan tarifaire cabinet (pricing volume)

---

## PHASE 6 : INTÉGRATION PDP / PPF & E-REPORTING `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase6_pdp.md`
> ⚠️ **DEADLINE : 1er Sept. 2026 (réception) / 1er Sept. 2027 (émission PME)**

- [ ] Étude et sélection d'une PDP immatriculée partenaire
- [ ] Intégration API PDP (émission factures via la PDP)
- [ ] Réception de factures électroniques (boîte de réception PDP)
- [ ] E-Reporting : Transmission données de transactions B2C / B2B international au PPF
- [ ] Gestion cycle de vie facture (Déposée → Acceptée → Rejetée → Payée)
- [ ] Enregistrement dans l'Annuaire PPF (identité de la plateforme)

---

## PHASE 7 : VERTICAL SAAS #1 (À DÉCIDER EN PHASE 3) `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase7_vertical.md`
> **Choix : BTP (recommandé) ou E-commerce**

### Si BTP
- [ ] Retenue de garantie (5% légal, libération à 1 an)
- [ ] Situations de travaux (facturation partielle sur avancement)
- [ ] Acomptes chantier
- [ ] Signature client électronique (devis → bon de commande)
- [ ] Suivi factures fournisseurs sous-traitants
- [ ] Mentions légales BTP spécifiques

### Si E-commerce
- [ ] Connecteur Shopify / WooCommerce / PrestaShop
- [ ] Factures auto à chaque commande
- [ ] Gestion avoirs (retours produits)
- [ ] Conformité marketplace (Amazon, etc.)

---

## PHASE 8 : SÉCURITÉ, TESTS & OBSERVABILITÉ `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase8_securite.md`
> En parallèle de toutes les phases (continu)

- [ ] Rate limiting + Helmet.js (OWASP)
- [ ] Validation stricte inputs (class-validator + Zod)
- [ ] Chiffrement données sensibles au repos
- [ ] RGPD : Registre des traitements + DPA sous-traitants
- [ ] Scan vulnérabilités (Dependabot + Snyk)
- [ ] Tests unitaires > 80% couverture (Logique TVA, Decimal)
- [ ] Tests intégration (Endpoints API)
- [ ] Tests conformité Factur-X (XML vs XSD)
- [ ] Tests E2E (Playwright — Flow création → génération → téléchargement)
- [ ] Logging structuré (Pino + format JSON)
- [ ] Sentry (NestJS + Next.js)
- [ ] Health checks (`/health`)

---

## PHASE 9 : OCR, IA & AUTOMATISATION `[ ]`
> Archive cible : `.memory/history/YYYY-MM-DD_phase9_ia.md`
> Post-MVP — Seulement après que le moteur est validé

- [ ] OCR factures fournisseurs (Import + reconnaissance automatique)
- [ ] Catégorisation IA (Produit/Service → Compte comptable)
- [ ] Relances automatiques (Emails horodatés factures impayées)
- [ ] Export FEC (Fichier des Écritures Comptables DGFiP)
- [ ] Rapports TVA (CA3 pré-remplie)
- [ ] Connecteurs comptables (API Cegid, Sage, Pennylane)
- [ ] Analytics (CA par client, par période, taux de paiement)
- [ ] PEPPOL (Réseau européen d'échange de factures)
