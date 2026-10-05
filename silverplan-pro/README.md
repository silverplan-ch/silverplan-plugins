# Plugin Silverplan Pro

L'agence Silverplan pour les **conseillers en prévoyance**. Même métier que le
plugin client, mais appliqué au dossier de vos clients — plus les compétences
propres au métier de conseiller.

Le plugin déclare son serveur MCP : l'installer branche les compétences **et**
votre portefeuille. Rien à ajouter à la main.

## Ce qu'il y a dedans

| | |
|---|---|
| `skills/silverplan` | l'orchestrateur : fait le point, nomme les mandats et les charge par `specialist_brief` |

Les mandats sont servis par le connecteur, jamais installés : les sept
mandats métier (retraite, 2ᵉ pilier, 3ᵉ pilier, financement immobilier,
impôts, transmission, décès et invalidité) et les trois du métier de
conseiller (revue de portefeuille, préparation de rendez-vous, mise en route
d'un client). `capabilities_list` rend ceux que votre rôle vous ouvre.

Différence de fond avec le plugin client : chaque appel désigne le client par
son `clientId`, l'agent produit une analyse de niveau conseiller, et **c'est le
conseiller qui décide et qui signe**. Aucune sortie ne part au client final
sans sa relecture : ni email, ni présentation, ni recommandation.

## Installer

### Claude Code / Cowork

```bash
/plugin marketplace add silverplan-ch/silverplan-plugins
```

```bash
/plugin install silverplan-pro@silverplan
```

Pour tester une version locale :

```bash
claude --plugin-dir ./packages/plugin-pro
```

L'autorisation OAuth se fait avec votre compte conseiller Silverplan.

### claude.ai (web) et Claude Desktop

Les plugins s'y installent aussi, avec leurs compétences. Sinon, le connecteur
seul (`https://www.silverplan.ch/api/mcp-pro`) donne les outils et les
parcours, sans les compétences.

## Modifier le contenu

Rien ne s'édite ici : tout est généré depuis `content/agents/`. Une fiche de
spécialiste porte ses outils pour les deux surfaces (`tools.user`,
`tools.pro`) et, si elle est réservée au conseiller, `surfaces: [pro]`.

```bash
npm run gen:agents
```

Guide complet : [`docs/AGENCY.md`](../../docs/AGENCY.md).
