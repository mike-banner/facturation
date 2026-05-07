# Database Tenancy & Isolation

## Principe
La plateforme est nativement multi-tenant. Chaque donnée appartient à une entreprise (`Company` ou `Organization`).

## Stratégie d'Isolation
- **Row-Level Isolation** : La plupart des tables possèdent une colonne `company_id` (UUID).
- **Filtrage Systématique** : Toutes les requêtes SQL/Prisma doivent inclure un filtre `where: { company_id: user.company_id }`.
- **Middleware/Intercepteurs** : Un intercepteur global dans NestJS doit injecter le `company_id` depuis le JWT dans le contexte de la requête pour garantir qu'aucune donnée ne fuite entre les tenants.

## Tables Globales
Seules les tables de configuration système ou les référentiels (ex: `vat_rates_standard`) peuvent être globales.

## Sécurité
- Interdiction des jointures qui ne valident pas le `company_id` sur les deux tables.
- Les tests d'intégration doivent inclure des scénarios de "Cross-tenant access" pour vérifier que l'accès est bloqué (403/404).
