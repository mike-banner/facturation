# Vision Produit — Orientée Moteur de Conformité

## Objectif Stratégique
Construire un **moteur de conformité fiscale (B2B)** — pas un logiciel de facture généraliste de plus.

## Le Positionnement Réel
```
COUCHE 3 — VERTICAL SAAS (produits marchands)
   BTP / Freelance / Santé / E-commerce / Experts-Comptables

COUCHE 2 — API PUBLIQUE (plateforme développeur)
   API Factur-X / API Conformité / Webhooks / Sandbox

COUCHE 1 — MOTEUR CONFORMITÉ (fondation technique, ce qu'on build d'abord)
   Génération XML EN16931 · PDF/A-3 · Validation · PAF · E-Reporting
```

## OÙ EST L'ARGENT (par potentiel réel)
| Modèle | Potentiel | Timing |
| :--- | :---: | :--- |
| API Conformité (Factur-X as a Service) | ⭐⭐⭐⭐⭐ | Phase 2 |
| White-label Experts-Comptables | ⭐⭐⭐⭐⭐ | Phase 3 |
| Vertical BTP | ⭐⭐⭐⭐⭐ | Phase 4 |
| Vertical E-commerce | ⭐⭐⭐⭐ | Phase 4 |
| Vertical Santé | ⭐⭐⭐⭐ | Phase 5 |
| OCR Comptable IA | ⭐⭐⭐⭐ | Phase 6 |
| SaaS Horizontal | ⭐⭐ | Jamais le focus |

## Anti-Objectifs (CE QU'ON NE FAIT PAS)
- ❌ "Encore un logiciel de facture généraliste" (marché saturé, pricing faible).
- ❌ Dashboard beau avant moteur solide.
- ❌ IA avant conformité.
- ❌ Microservices partout.
- ❌ Toutes les verticales en même temps.

## Vertical #1 : À choisir APRÈS que le moteur est validé
Candidats prioritaires selon critères (taille marché + douleur + pricing) :
1. **Experts-Comptables** → Clients captifs, volume élevé, pricing B2B fort, transition 2026 urgente.
2. **BTP** → Cas d'usage complexes (retenue garantie, acomptes chantier, situations de travaux) → Moat défensif.

> **Décision à prendre en Phase 3** après validation du moteur.
# Stratégie de Monétisation & Positionnement

## Le Principe Fondateur
> Construire **une seule fois** un moteur de conformité robuste. Le monétiser **de plusieurs façons** en parallèle.

## Les 3 Vecteurs de Revenus

### Vecteur 1 — API Conformité (Developer-First)
Exposer le moteur Factur-X en tant que service consommable via API.

| Aspect | Détail |
| :--- | :--- |
| **Produit** | API REST + SDK (JS/Python) pour générer des Factur-X, valider des XML EN16931, créer des PDF/A-3. |
| **Cible** | Développeurs d'ERP, e-commerce, logiciels métier qui ont besoin de conformité sans la construire. |
| **Pricing** | Pay-as-you-go (par facture générée) + abonnements volumes. |
| **Moat** | Documentation excellente, SLA, Sandbox de test, Certification PDP future. |
| **Timeline** | Phase 2 du plan. |

### Vecteur 2 — White-Label Experts-Comptables
Fournir la plateforme en marque blanche aux cabinets comptables.

| Aspect | Détail |
| :--- | :--- |
| **Produit** | Plateforme rebrandée sous le nom du cabinet, multi-clients gérés par le cabinet. |
| **Cible** | Cabinets comptables (transition 2026 obligatoire, ils sont dépassés). |
| **Pricing** | Abonnement mensuel par cabinet (volume de factures inclus). |
| **Moat** | Intégrations logiciels comptables (Cegid, Sage, Quadratus). |
| **Timeline** | Phase 3 du plan. |

### Vecteur 3 — Vertical SaaS Métier
Wrapper vertical au-dessus du moteur avec des fonctionnalités spécifiques à un secteur.

| Vertical | Différenciateur spécifique | Potentiel |
| :--- | :--- | :---: |
| **BTP** | Retenue de garantie, acomptes chantier, situations de travaux, signature client. | ⭐⭐⭐⭐⭐ |
| **E-commerce** | Sync Shopify/WooCommerce, factures auto à la commande, retours/avoirs. | ⭐⭐⭐⭐ |
| **Santé** | Nomenclatures CCAM/NGAP, tiers payant, conformité RPPS. | ⭐⭐⭐⭐ |
| **Transport** | Lettres de voiture, suivi livraisons, factures multi-destinataires. | ⭐⭐⭐ |

## Ce Qu'on NE Vend PAS
- ❌ Un logiciel de facturation généraliste (Freepik, Zervant, QuickBooks) → Guerre de prix, pas de moat.

## Séquençage Stratégique
```
MAINTENANT → Construire le Moteur (Phases 1-2)
Q3 2026   → Ouvrir l'API publique (Phase 2) — Deadline Réforme
Q4 2026   → White-label Experts-Comptables (Phase 3)
2027      → Vertical #1 (BTP ou E-commerce, à décider Phase 3)
2027+     → Expansion verticales / OCR IA
```
