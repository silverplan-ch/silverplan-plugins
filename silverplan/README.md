# Plugin Silverplan

L’assistant Silverplan s’appuie sur votre dossier financier et sur le moteur
de projection suisse. Le plugin installe ses instructions et connecte votre
dossier au serveur MCP Silverplan.

## Ce qu'il y a dedans

| | |
|---|---|
| `skills/silverplan` | les instructions et les outils de l’assistant |
| `.claude-plugin/plugin.json` | le manifeste, dont la déclaration du serveur MCP |

Les **outils** — dossier, moteur de
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
`silverplan-pro` (`packages/plugin-pro/`), qui donne accès aux outils de
conseil et aux dossiers de leurs clients sur `/api/mcp-pro`.

## Modifier le contenu

Rien ne s'édite ici : tout est généré.

| Ce que vous voulez changer | Le fichier à éditer |
|---|---|
| le nom, la version, la description, l'URL du serveur | `content/agents/plugin.md` |
| la voix et le rôle de l’assistant | `content/agents/orchestrator.md` |
| les règles communes (honnêteté des chiffres, escalade) | `content/agents/sections/` |
| les produits d'un partenaire, sa voix et ses garde-fous | la console partenaire, sans déploiement |

Puis :

```bash
npm run gen:agents
```

La CI vérifie qu'aucune sortie générée n'a dérivé de sa source
(`npm run gen:agents:check`).

Guide complet — configurer, publier, vérifier : [`docs/AGENT_PLATFORM.md`](../../docs/AGENT_PLATFORM.md#assistant-instructions-and-journeys).

## Vérifier que la chaîne tient

```bash
npm run verify:plugin:live
```

Manifeste, compétences, entrée de place de marché, puis le serveur déclaré :
métadonnées OAuth et poignée de main non authentifiée.
