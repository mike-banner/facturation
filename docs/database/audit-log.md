# Database Audit Logging

## Objectif
Maintenir une Piste d'Audit Fiable (PAF) pour la conformité fiscale et la sécurité.

## Événements à Logguer
Toute action d'écriture (`INSERT`, `UPDATE`, `DELETE`) sur les entités suivantes doit générer une entrée d'audit :
- `Invoices`
- `Payments`
- `Company Settings`
- `User Permissions`

## Structure du Log
Chaque entrée d'audit doit contenir :
- `id` (UUID)
- `timestamp` (UTC)
- `user_id`
- `company_id`
- `action` (CREATE, UPDATE, DELETE, SEND, PAY)
- `entity_type` (ex: "INVOICE")
- `entity_id`
- `changes` (JSONB) : Valeurs avant/après pour les updates.
- `metadata` (JSONB) : IP, User-Agent, etc.

## Immuabilité des Logs
Les logs d'audit sont strictement **Append-only**. Aucun `UPDATE` ou `DELETE` n'est autorisé sur cette table.
