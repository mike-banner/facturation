# Schema: Companies

## Description
Représente une entité légale (entreprise) sur la plateforme.

## Champs
| Champ | Type | Description | Règle |
| :--- | :--- | :--- | :--- |
| `id` | UUID | Clé primaire | - |
| `name` | VARCHAR | Nom de l'entreprise | Requis |
| `siren` | VARCHAR(9) | Numéro SIREN | Unique, 9 chiffres |
| `siret` | VARCHAR(14) | Numéro SIRET | Optionnel (siège) |
| `vat_number` | VARCHAR | Numéro de TVA intracommunautaire | Format FR+2 chiffres+SIREN |
| `address_line1`| VARCHAR | Adresse | Requis |
| `address_line2`| VARCHAR | Complément d'adresse | - |
| `zip_code` | VARCHAR | Code postal | Requis |
| `city` | VARCHAR | Ville | Requis |
| `country` | VARCHAR | Pays (ISO 3166-1 alpha-2) | Défaut: 'FR' |
| `created_at` | TIMESTAMPTZ | Date de création | Auto |
| `updated_at` | TIMESTAMPTZ | Date de mise à jour | Auto |

## Relations
- `Users`: Has many.
- `Invoices`: Has many.
- `Customers`: Has many.
