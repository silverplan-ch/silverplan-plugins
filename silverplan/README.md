# Plugin Silverplan

L'agence de conseil Silverplan dans un assistant : un orchestrateur et sept
compétences spécialisées, adossés au dossier financier du client et au moteur
de projection suisse.

Le plugin déclare lui-même le serveur MCP Silverplan : l'installer branche les
compétences **et** le dossier. Il n'y a pas de connecteur à ajouter à la main.

## Ce qu'il y a dedans

| | |
|---|---|
| `skills/silverplan` | l'orchestrateur : fait le point sur le dossier, nomme les mandats et les charge par `specialist_brief` |
| `.claude-plugin/plugin.json` | le manifeste, dont la déclaration du serveur MCP |

Les mandats (prévoyance, 2ᵉ pilier, 3ᵉ pilier, financement immobilier,
impôts, transmission, décès et invalidité) ne sont pas installés : le serveur
les sert à la demande, toujours à jour. Un mandat dit à l'assistant **comment**
se comporter dans un domaine (ce qu'il établit d'abord, ses frontières, quand
il passe la main, quand il escalade vers un conseiller humain). Les **outils** — dossier, moteur de
projection, scénarios, extraction de documents, fiches produits — vivent sur le
serveur Silverplan et sont appelés par MCP. Les chiffres viennent du moteur,
jamais du modèle.

## Installer

### Claude Code / Cowork

```bash
/plugin marketplace add silverplan-ch/silverplan-plugins
```

```bash
/plugin install silverplan@silverplan
```

Pour tester une version locale sans passer par la place de marché :

```bash
claude --plugin-dir ./packages/plugin
```

À la première utilisation d'un outil, Claude ouvre l'autorisation OAuth : vous
vous connectez avec votre compte Silverplan, et tout est épinglé sur ce
compte-là.

### claude.ai (web) et Claude Desktop

Les plugins s'installent aussi dans le chat web et dans Claude Desktop, avec
leurs compétences. Un skill seul peut également être ajouté en ZIP depuis
Customize → Skills.

Si vous préférez le connecteur seul (Réglages → Connecteurs → Ajouter un
connecteur custom, URL `https://www.silverplan.ch/api/mcp-user`), vous obtenez
les outils et les parcours publiés par le serveur, sans les compétences.

### ChatGPT

Mode développeur → ajouter un connecteur MCP, même URL : les outils et les
parcours, sans les compétences. Les plugins ChatGPT acceptent aussi
compétences + MCP, mais Silverplan n'y est pas encore publié.

## Le plugin conseiller

Ce paquet est le plugin **client**. Les conseillers installent
`silverplan-pro` (`packages/plugin-pro/`) : mêmes compétences métier appliquées
au dossier de leurs clients, plus les compétences du métier de conseiller, sur
la surface `/api/mcp-pro`.

## Modifier le contenu

Rien ne s'édite ici : tout est généré.

| Ce que vous voulez changer | Le fichier à éditer |
|---|---|
| le nom, la version, la description, l'URL du serveur | `content/agents/plugin.md` |
| la voix d'accueil, l'annuaire des spécialistes | `content/agents/orchestrator.md` |
| les règles communes (honnêteté des chiffres, escalade) | `content/agents/core.md` |
| le mandat d'un spécialiste, ses outils, ses frontières | `content/agents/specialists/<id>.md` |
| les produits d'un partenaire, sa voix et ses garde-fous | la console partenaire, sans déploiement |

Puis :

```bash
npm run gen:agents
```

La CI vérifie qu'aucune sortie générée n'a dérivé de sa source
(`npm run gen:agents:check`).

Guide complet — configurer, publier, vérifier : [`docs/AGENCY.md`](../../docs/AGENCY.md).

## Vérifier que la chaîne tient

```bash
npm run verify:plugin:live
```

Manifeste, compétences, entrée de place de marché, puis le serveur déclaré :
métadonnées OAuth et poignée de main non authentifiée.
