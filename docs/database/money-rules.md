# Database Money Rules — ZERO FLOAT POLICY

## 1. Stockage (PostgreSQL)
- Tous les montants monétaires (prix unitaire, totaux, taxes) doivent utiliser le type `NUMERIC(18,4)`.
- Ne jamais utiliser `REAL`, `DOUBLE PRECISION` ou `FLOAT`.

## 2. Calculs (Backend NestJS)
- **Interdiction formelle** de réaliser des calculs financiers avec les opérateurs natifs (`+`, `-`, `*`, `/`) sur des types `number`.
- Utilisation obligatoire de la librairie **`decimal.js`**.
- Tous les calculs de taxes et de totaux doivent être effectués côté backend.

## 3. Précision et Arrondis
- Les calculs intermédiaires sont effectués avec **4 décimales**.
- L'arrondi final pour l'affichage et la facturation légale se fait au **centime le plus proche** (2 décimales) selon la norme ISO (arrondi arithmétique).

## 4. Transmission (API)
- Les montants sortants sont convertis en `string` pour préserver la précision côté client.

---
*Tout non-respect de ces règles entraînera un rejet immédiat de la PR.*
