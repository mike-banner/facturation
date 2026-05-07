# API Authentication

## Strategy
L'API utilise **Supabase Auth** pour la gestion des utilisateurs et des sessions.

## Authentication Methods
1. **JWT (Mobile & Web App)** : Le client doit fournir un `AccessToken` dans le header Authorization.
   - Header : `Authorization: Bearer <JWT_TOKEN>`
2. **API Keys (Developer API)** : Pour l'accès programmatique.
   - Header : `X-API-KEY: <YOUR_SECRET_KEY>`

## RBAC (Role-Based Access Control)
Chaque utilisateur possède un rôle au sein d'une entreprise :
- `OWNER` : Accès total.
- `ADMIN` : Accès total sauf billing.
- `EDITOR` : Création/Édition.
- `VIEWER` : Lecture seule.

## Security
- Les tokens ont une durée de vie courte (1h).
- Le `RefreshToken` est utilisé pour obtenir un nouveau JWT.
