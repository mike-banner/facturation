# Modules du MVP

## Liste des Modules

| Module | Priorité | Statut CTO |
| :--- | :--- | :--- |
| **Authentification** | Critique | Base absolue (Supabase). |
| **Entreprises** | Critique | Entité racine (Siren, TVA, Adresse). |
| **Clients** | Critique | Nécessaire pour émettre une facture. |
| **Produits/services** | Critique | Catalogue de base (nom, prix HT, taux TVA). |
| **Factures** | Critique | Le cœur du système. |
| **PDF** | Critique | Doit être au format **PDF/A-3** (Obligation légale). |
| **Factur-X XML** | Critique | Fichier XML encapsulé selon EN16931. |
| **Devis** | Important | Transformation facile en facture. |
| **Dashboard** | Important | Vue d'ensemble (CA, Factures en attente). |
| **Logs audit** | Important | Piste d'audit fiable (Immutabilité). |

## À exclure formellement du MVP
- Comptabilité avancée (Grand livre, Lettrage).
- Statut PDP complet (qui demande des audits de sécurité et certifications lourdes).
- IA de catégorisation ou de prédiction.
