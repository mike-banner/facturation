# RULES — Gouvernance d'Architecture & IA

## Règle d'Or
La documentation dirige le code. Le code ne dirige jamais la documentation.
L'IA est un assistant technique sous supervision stricte. Elle ne possède pas l'autorité finale sur les choix structurants.

## 1. Interdictions Strictes (Hard Locks)
Il est formellement **INTERDIT** à l'IA de réaliser les actions suivantes sans une **ADR validée** et une **approbation explicite** (validation par "Go" ou "Approved") :
- **Stack** : Changer de langage, de framework ou de base de données (PostgreSQL obligatoire).
- **Architecture** : Créer des microservices (hors Worker Python), ajouter un orchestrateur (K8s), ou refactoriser le pattern API-First.
- **Base de Données** : Modifier les modèles financiers ou les types de données critiques (`NUMERIC/Decimal`).
- **Dépendances** : Ajouter une librairie majeure (ex: passage de Prisma à TypeORM, ajout d'un moteur de queue différent de Redis).

## 2. Standards de Développement
- **Finance** : Zéro Float. Utilisation obligatoire de `Decimal` (Postgres `NUMERIC(18,4)`).
- **Backend** : NestJS est la source unique de vérité pour la logique métier et fiscale.
- **Frontend** : Next.js (SaaS) et Astro (Marketing) sont strictement limités à l'affichage.
- **Compliance** : Factur-X / PDF/A-3 via Worker Python uniquement.
- **API** : Toute nouvelle route doit être documentée (OpenAPI) avant son implémentation.

## 3. Procédure de Changement
Toute proposition d'évolution structurante doit suivre ce workflow :
1. **Signalement** : L'IA expose le besoin de changement.
2. **ADR** : Création d'un fichier `docs/adr/ADR-XXX-nom.md`.
3. **Validation** : Attente de l'approbation explicite de l'utilisateur.
4. **Implémentation** : Une fois validé, mise à jour de `docs/MASTER_PLAN.md` et exécution.

## 4. Gouvernance & Historique
- Toute action critique (fin de phase, décision majeure) doit être logguée dans `docs/history/`.
- La documentation doit être tenue à jour en temps réel. Une incohérence entre la doc et le code est considérée comme un bug prioritaire.

---
*Le non-respect de ces règles sera considéré comme une régression majeure de l'architecture.*
