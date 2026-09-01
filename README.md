# SilverPlan pour votre assistant IA

Une agence de conseil en prévoyance suisse, dans Claude ou ChatGPT. Les
chiffres viennent d'un moteur de projection déterministe, jamais du modèle.

Deux plugins, pour deux métiers.

| | **SilverPlan** | **SilverPlan Pro** |
|---|---|---|
| Pour qui | un particulier, sur son propre dossier | un conseiller, sur le dossier de ses clients |
| Compétences | 8 | 11 |
| Il faut | un compte SilverPlan | un compte conseiller SilverPlan |

## Ce que ça sait faire

Un orchestrateur accueille, comprend le sujet, puis passe la main à la
compétence concernée : **prévoyance** (vue d'ensemble retraite), **2ᵉ pilier**
(certificat, rachats, rente ou capital), **3ᵉ pilier** (plafond, versement
soutenable, économie d'impôt), **hypothèque** (fonds propres, capacité,
amortissement), **fiscalité** (déductions ouvertes, échéances),
**succession** (inventaire, régime matrimonial, bénéficiaires) et
**assurance vie** (décès, invalidité, lacune du ménage).

Le plugin conseiller ajoute trois compétences propres à son métier :
**revue de portefeuille** (qui rappeler, quels dossiers stagnent, quelles
opportunités), **préparation de rendez-vous** (points du dossier, scénarios à
projeter, présentation et message) et **onboarding client** (créer, inviter,
suivre la collecte).

### Quelques demandes qui marchent

Côté particulier :

- « Je peux prendre ma retraite à 62 ans ? »
- « Voici mon certificat LPP. » (déposez le PDF : les valeurs entrent au dossier avec leur source)
- « Et si j'achetais un appartement à 700 000 avant ? »
- « Qu'est-ce qu'il te manque pour être sûr ? »

Côté conseiller :

- « Par quels clients devrais-je commencer cette semaine ? »
- « Prépare mon rendez-vous de jeudi avec ce client. »
- « Ce prospect m'a laissé ses coordonnées : mets-le en route. »

## Installer

### Dans Claude (Claude Code, Cowork, claude.ai, Desktop)

Depuis ce dépôt, en une commande tapée **dans la conversation Claude** (pas
dans un terminal) :

```
/plugin marketplace add <ce-depot>
```

Puis, selon votre métier :

```
/plugin install silverplan@silverplan
```

```
/plugin install silverplan-pro@silverplan
```

### Depuis un fichier

Les deux plugins sont aussi distribués en `.zip`. Dans Cowork : Plugins →
installer depuis un fichier. En local, sans rien installer :

```bash
claude --plugin-dir ./silverplan
```

### La connexion à votre dossier

À la première utilisation d'un outil, Claude ouvre une autorisation : vous
vous connectez avec votre compte SilverPlan. Tout est ensuite épinglé sur ce
compte — un particulier ne voit que son dossier, un conseiller que son
portefeuille.

### ChatGPT

Ajoutez le connecteur en mode développeur (Paramètres → Apps & Connectors) :
`https://www.silverplan.ch/api/mcp-user` pour un particulier,
`https://www.silverplan.ch/api/mcp-pro` pour un conseiller. Vous obtenez les
outils et les parcours guidés ; les compétences spécialisées ci-dessus ne
sont pas encore publiées sur ChatGPT.

## Comment c'est construit

Trois couches, et une seule fait autorité sur chaque chose :

- **Les compétences** (ce dépôt) disent *comment se comporter* : ce que l'agent
  établit d'abord, ses frontières, quand il passe la main, quand il escalade
  vers un humain. Ce sont des fichiers Markdown, lus par votre assistant.
- **Les outils** restent sur le serveur SilverPlan : le dossier, le moteur de
  projection suisse, les scénarios, l'extraction de documents. L'assistant les
  appelle, il ne les héberge pas.
- **Le dossier** est la mémoire. Ni l'assistant ni sa mémoire de conversation
  ne font autorité : ce qu'il croit savoir de vous n'entre au dossier qu'après
  votre confirmation, avec sa provenance.

Conséquence pratique : un chiffre affiché est calculé, pas rédigé. Si le
dossier ne permet pas de calculer, l'agent le dit et demande ce qui manque —
il n'invente pas.

## Ce que l'agent ne fait pas

- Il ne recommande pas un produit automatiquement : il explique, qualifie, et
  oriente vers un conseiller humain.
- Il ne prend aucune décision engageante à votre place.
- Côté conseiller, rien ne part au client final sans relecture : ni email, ni
  présentation, ni recommandation.

## Mise à jour

```
/plugin update silverplan
```

Les compétences voyagent ; les outils et votre dossier étaient déjà côté
serveur, il n'y a rien d'autre à mettre à jour.

---

Ces plugins sont générés depuis une source unique. Ne les éditez pas à la
main : une modification serait écrasée à la publication suivante.
