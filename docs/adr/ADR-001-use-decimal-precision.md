# ADR-001 : Utilisation de la Précision Décimale Stricte

## Contexte
Les calculs financiers en JavaScript avec le type natif `Number` (Float IEEE 754) produisent des erreurs d'arrondis (ex: `0.1 + 0.2 = 0.30000000000004`). En comptabilité et facturation, ces erreurs sont inadmissibles et peuvent invalider la conformité fiscale.

## Décision
Bannissement total des types `Float`, `Double` et `Number` pour tout montant monétaire ou taux de taxe.
Utilisation systématique de :
- **Base de données** : `NUMERIC(18,4)` (PostgreSQL).
- **ORM** : Type `Decimal` (Prisma).
- **Code Backend** : Librairie `decimal.js` (NestJS).

## Alternatives
- `Int` (centimes) : Moins flexible pour les taux de TVA précis (ex: 5.5%) ou les prix unitaires à haute précision.
- `Float` : Rejeté pour manque de précision.

## Conséquences
- Plus de sécurité et de précision comptable.
- Nécessité de convertir les données lors des échanges avec le Frontend (qui ne fait que de l'affichage).
- Légère surcharge de calcul, négligeable face au gain de fiabilité.

## Statut
Accepted
