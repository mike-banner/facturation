# Schema: Invoices

## Description
Représente une facture émise.

## Champs
| Champ | Type | Description | Règle |
| :--- | :--- | :--- | :--- |
| `id` | UUID | Clé primaire | - |
| `company_id` | UUID | FK vers Companies | Multi-tenant |
| `customer_id` | UUID | FK vers Customers | Requis |
| `invoice_number`| VARCHAR | Numéro de facture (ex: FAC-2026-001) | Unique par Company |
| `status` | ENUM | État de la facture | `DRAFT`, `SENT`, `PAID`, `CANCELLED`, `OVERDUE` |
| `issue_date` | DATE | Date d'émission | - |
| `due_date` | DATE | Date d'échéance | - |
| `total_ht` | NUMERIC(18,4)| Total Hors Taxes | Decimal |
| `total_tva` | NUMERIC(18,4)| Total TVA | Decimal |
| `total_ttc` | NUMERIC(18,4)| Total Toutes Taxes Comprises | Decimal |
| `currency` | VARCHAR(3) | Devise | ISO 4217 (Défaut: 'EUR') |
| `is_facturx` | BOOLEAN | Si le document Factur-X a été généré | Défaut: false |
| `file_path_s3` | VARCHAR | Chemin vers le PDF/A-3 sur S3 | - |
| `created_at` | TIMESTAMPTZ | Date de création | Auto |
| `updated_at` | TIMESTAMPTZ | Date de mise à jour | Auto |

## Relations
- `InvoiceLines`: Has many.
- `Company`: Belongs to.
- `Customer`: Belongs to.

## Règles Métier
- Une fois en statut `SENT` ou `PAID`, la facture devient **immuable**.
- Le `invoice_number` doit suivre une séquence continue (obligation légale).
