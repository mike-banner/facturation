# Règles Comptables et Types de Données

## Le Dogme des Décimales
L'utilisation de `Float`, `Double` ou `Number` JS pour manipuler des montants financiers est **strictement interdite** (problème inhérent à la norme IEEE 754, ex: `0.1 + 0.2 = 0.30000000000004`).

## Stack de Précision
Pour garantir une comptabilité au centime près et auditable :
1. **PostgreSQL** : `NUMERIC(18,4)`
2. **Prisma ORM** : `Decimal`
3. **Backend NestJS** : Librairie `decimal.js`
4. **Calculs** : Exécutés à 100% côté backend (le front-end n'a qu'un rôle d'affichage).

## Structure Comptable Standard
Tous les modèles liés à la facturation doivent implémenter :
- `unit_price` (Decimal)
- `vat_rate` (Decimal)
- `total_ht` (Decimal)
- `total_tva` (Decimal)
- `total_ttc` (Decimal)
