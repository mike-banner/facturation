# ADR-002 : Délégation Documentaire via Worker Python

## Contexte
La génération de fichiers PDF/A-3 (avec embedding XML) et le respect de la norme Factur-X sont techniquement complexes. L'écosystème Node.js manque de librairies matures pour le PDF/A-3 et le XML EN16931 complexe par rapport à Python ou Java.

## Décision
Utilisation d'un microservice ultra-spécifique (Worker) en Python dédié à la génération de documents.
- NestJS pousse les données dans **Redis (BullMQ)**.
- Le **Worker Python** génère le XML (lxml), compile le PDF/A-3 (Ghostscript) et effectue l'embedding.

## Alternatives
- Librairies JS (pdf-lib, etc.) : Trop limitées pour le PDF/A-3 et Factur-X.
- Java : Performant mais plus lourd à déployer et maintenir que Python pour ce cas d'usage.

## Conséquences
- Isolation de la charge CPU lourde.
- Nécessité de maintenir deux environnements (Node.js et Python).
- Robustesse accrue via le système de file d'attente (Redis).

## Statut
Accepted
