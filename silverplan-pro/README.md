# Plugin Silverplan Pro

L’assistant Silverplan pour les **conseillers en prévoyance** s’appuie sur
les dossiers de vos clients. Le plugin installe ses instructions et connecte
votre portefeuille au serveur MCP Silverplan.

## Ce qu'il y a dedans

| | |
|---|---|
| `skills/silverplan` | les instructions et les outils de l’assistant |

Différence de fond avec le plugin client : chaque appel désigne le client par
son `clientId`, l'agent produit une analyse de niveau conseiller, et **c'est le
conseiller qui décide et qui signe**. Un agent externe n'envoie au client
final que si le conseiller lui en a donné l'accord permanent. Sans cet accord,
l'envoi est bloqué. Les envois pris en charge sont conservés pour validation
dans Silverplan, les autres sont refusés.

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

Rien ne s'édite ici : tout est généré depuis `content/agents/`. Les outils propres à chaque surface sont définis dans `orchestrator.md`.

```bash
npm run gen:agents
```

Guide complet : [`docs/AGENT_PLATFORM.md`](../../docs/AGENT_PLATFORM.md#assistant-instructions-and-journeys).
