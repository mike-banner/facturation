# API: Create Invoice

## Endpoint
`POST /invoices`

## Description
Crée une nouvelle facture en brouillon (`DRAFT`). Calcule automatiquement les totaux à partir des lignes fournies.

## Request Body
| Champ | Type | Obligatoire | Description |
| :--- | :--- | :---: | :--- |
| `customer_id` | UUID | Oui | ID du client |
| `issue_date` | DATE | Non | Date d'émission (Défaut: aujourd'hui) |
| `due_date` | DATE | Non | Date d'échéance |
| `lines` | Array | Oui | Liste des lignes de facture |

### Object: Line
| Champ | Type | Description |
| :--- | :--- | :--- |
| `description` | String | Description du service |
| `quantity` | String (Decimal) | Quantité (ex: "2.0") |
| `unit_price` | String (Decimal) | Prix HT (ex: "150.00") |
| `vat_rate` | String (Decimal) | Taux de TVA (ex: "20.0") |

## Example Request
```json
{
  "customer_id": "550e8400-e29b-41d4-a716-446655440000",
  "lines": [
    {
      "description": "Consulting prestation",
      "quantity": "1.0",
      "unit_price": "1000.00",
      "vat_rate": "20.0"
    }
  ]
}
```

## Example Response (`201 Created`)
```json
{
  "id": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11",
  "invoice_number": "FAC-2026-001",
  "status": "DRAFT",
  "total_ht": "1000.00",
  "total_tva": "200.00",
  "total_ttc": "1200.00",
  "created_at": "2026-05-07T14:00:00Z"
}
```

## Erreurs spécifiques
- `400 CUSTOMER_NOT_FOUND` : Le client n'existe pas.
- `400 INVALID_DECIMAL` : Format de nombre invalide.
