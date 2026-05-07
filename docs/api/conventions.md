# API Conventions

## Naming
- **Resources**: Plural nouns (e.g., `/invoices`, `/customers`).
- **Fields**: `snake_case` for all JSON keys.

## Dates
- All dates must be in **ISO 8601** format (UTC).
- Format: `YYYY-MM-DDTHH:mm:ssZ`.

## Money & Numbers
- **RÈGLE CRITIQUE** : Les montants monétaires ne doivent **JAMAIS** être des types `number` (float) en JSON.
- Les montants sont transmis sous forme de **string** avec 2 ou 4 décimales.
- Exemple : `{ "total_ht": "125.50" }`.

## Pagination
- Cursor-based pagination is preferred for large collections.
- Parameters: `cursor`, `limit`.

## HTTP Status Codes
- `200 OK` : Succès.
- `201 Created` : Ressource créée.
- `202 Accepted` : Job asynchrone démarré (ex: génération Factur-X).
- `400 Bad Request` : Erreur de validation.
- `401 Unauthorized` : Authentification manquante ou invalide.
- `403 Forbidden` : Droits insuffisants.
- `404 Not Found` : Ressource inexistante.
- `429 Too Many Requests` : Rate limit atteint.
- `500 Internal Server Error` : Erreur serveur.

## Identifier Format
- Tous les IDs sont des **UUID v4**.
