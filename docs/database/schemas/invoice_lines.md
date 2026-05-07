# Schema: InvoiceLines

## Description
Lignes de détail d'une facture.

## Champs
| Champ | Type | Description | Règle |
| :--- | :--- | :--- | :--- |
| `id` | UUID | Clé primaire | - |
| `invoice_id` | UUID | FK vers Invoices | Requis |
| `description` | TEXT | Description du produit/service | Requis |
| `quantity` | NUMERIC(18,4)| Quantité | Decimal |
| `unit_price` | NUMERIC(18,4)| Prix unitaire HT | Decimal |
| `vat_rate` | NUMERIC(18,4)| Taux de TVA (ex: 20.0000) | Decimal |
| `total_ht` | NUMERIC(18,4)| Total HT de la ligne | Decimal (qty * price) |
| `total_tva` | NUMERIC(18,4)| Total TVA de la ligne | Decimal |
| `total_ttc` | NUMERIC(18,4)| Total TTC de la ligne | Decimal |

## Règles de Calcul
- `total_ht = quantity * unit_price`
- `total_tva = total_ht * (vat_rate / 100)`
- `total_ttc = total_ht + total_tva`
- Tous les calculs sont faits avec la précision de `decimal.js`.
