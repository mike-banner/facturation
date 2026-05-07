# Compliance France / EU — Obligations Légales

## CADRE LÉGAL : Ce que l'État attend (2026-2027)

### Calendrier Obligatoire
| Date | Obligation | Cible |
| :--- | :--- | :--- |
| **1er Sept. 2026** | Réception factures électroniques | **Toutes entreprises** (TVA) |
| **1er Sept. 2026** | Émission factures électroniques | Grandes Entreprises (GE) + ETI |
| **1er Sept. 2027** | Émission factures électroniques | **PME + Micro-entreprises** |

> ⚠️ Notre SaaS doit être **opérationnel et compliant avant le 1er Sept. 2026** pour les PME/TPE qui doivent recevoir.

---

## ARCHITECTURE RÉGLEMENTAIRE (PDP / PPF)

### Rôles des acteurs
| Acteur | Rôle | Impact sur notre SaaS |
| :--- | :--- | :--- |
| **PPF** (Portail Public Facturation) | Annuaire centralisé + concentrateur de données vers DGFiP | Nous devons être capables de lui envoyer les données (e-reporting) |
| **PDP** (Plateforme Dématérialisation Partenaire) | Émettre/Recevoir les factures, contrôler la conformité, transmettre les données à l'État | Notre cible long terme : devenir PDP ou s'interfacer avec une PDP |
| **Notre SaaS (Phase 1-4)** | Génération de factures Factur-X pour PME | Interface avec une PDP tierce immatriculée |

---

## EXIGENCES TECHNIQUES OBLIGATOIRES

### Format des Factures
| Norme | Description | Obligatoire |
| :--- | :--- | :---: |
| **EN 16931** | Norme sémantique européenne (contenu de la facture) | ✅ |
| **Factur-X** | Format hybride PDF/A-3 + XML CII (norme française préférée) | ✅ |
| **UBL 2.1** | Format XML alternatif (accepté par les PDP) | Supporté |
| **PDF/A-3** | Contenant obligatoire (PDF archivage) | ✅ |

### Données obligatoires sur chaque facture (DGFiP)
- SIREN/SIRET de l'émetteur
- Numéro de TVA intracommunautaire
- Numéro de facture (séquence non-interrompue, non-réutilisable)
- Date d'émission
- Date d'exécution de la prestation/livraison
- Identité complète du client
- Détail des lignes (HT + Taux TVA + Montant TVA)
- Total HT / Total TVA / Total TTC
- Conditions de règlement (délai, mode, pénalités de retard)
- Mentions légales (auto-entrepreneur, TVA non applicable si cas de franchise)

### Piste d'Audit Fiable (PAF) — Loi Anti-Fraude TVA 2018
- L'entreprise doit prouver le chemin de la facture de la création au paiement.
- Notre implémentation : Logs immuables, statuts horodatés, aucune suppression possible.

### Conservation Légale
- **10 ans minimum** après clôture de l'exercice fiscal.
- Format : Les PDF/A-3 doivent être archivés sur S3 avec une politique de rétention.
- Accessibilité : Données lisibles et exportables sur demande de l'administration.

### E-Reporting
Pour les opérations B2C ou B2B internationales (hors obligation facture électronique), l'entreprise doit transmettre des **données de transaction** à la DGFiP.
- Fréquence : Selon régime TVA (mensuel ou trimestriel).
- Transmission : Via une PDP ou directement au PPF.

### RGPD
- DPA (Data Processing Agreement) avec chaque sous-traitant.
- Droit à l'effacement : Attention ! Conflit avec l'obligation de conservation 10 ans. Solution : Anonymiser (pseudonymiser) les données personnelles, pas les supprimer.
- Chiffrement des données sensibles au repos (S3, PostgreSQL).
- Registre des traitements.
