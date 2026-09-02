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

### Exemples d'interactions

Vous écrivez en français, normalement. L'agent choisit lui-même le spécialiste
et les outils.

**Pour un particulier**

| Vous demandez | Ce que vous obtenez |
|---|---|
| « Je peux prendre ma retraite à 62 ans ? » | Les deux trajectoires chiffrées côte à côte : capital à la retraite, capital en fin de vie, revenu mensuel, impôts |
| « Et si j'achetais un appartement à 700 000 ? » | Les fonds propres exigés, la charge mensuelle, le taux d'effort, et si la banque suivrait |
| « Qu'est-ce qu'il te manque pour être sûr ? » | La liste précise des champs vides de votre dossier, et pour chacun le document qui le remplirait |
| « Voici mon certificat LPP » (PDF déposé) | Les valeurs lues et versées au dossier, chacune rattachée à sa page d'origine |

**Pour un conseiller**

| Vous demandez | Ce que vous obtenez |
|---|---|
| « Par quels clients commencer cette semaine ? » | Votre portefeuille trié, avec pour chacun le nombre de jours depuis la dernière mise à jour |
| « Qu'est-ce qui cloche chez ce client ? » | Les lacunes détectées par le moteur, chiffrées — par exemple : capital décès de 0 CHF face à une hypothèque de 445 000, ou couverture invalidité à 54 % |
| « Qui est en retard sur ses documents ? » | Pour chaque client, ce qui a été demandé, reçu, et ce qui manque encore |
| « Prépare mon rendez-vous avec ce client » | Les points du dossier, les scénarios à projeter, un brouillon de présentation et de message |

## Installer

### Dans Claude

Fonctionne partout : Claude Code, Cowork, claude.ai et l'application de
bureau.

Tapez ces deux lignes **dans la conversation Claude** — ce sont des commandes
de Claude, pas de votre terminal. La première déclare le dépôt, une fois pour
toutes. La seconde installe le plugin qui vous concerne.

```
/plugin marketplace add ndengler/silverplan-plugins
```

```
/plugin install silverplan@silverplan
```

Un conseiller installe `silverplan-pro@silverplan` à la place.

Si vous préférez un fichier, les deux plugins se téléchargent aussi :
[silverplan.zip](https://www.silverplan.ch/plugins/silverplan.zip) ·
[silverplan-pro.zip](https://www.silverplan.ch/plugins/silverplan-pro.zip).
Dans Claude : Plugins → installer depuis un fichier.

### Dans ChatGPT

Paramètres → Apps & Connectors → Developer Mode → ajouter un connecteur, avec
l'une de ces adresses :

```
https://www.silverplan.ch/api/mcp-user     (particulier)
https://www.silverplan.ch/api/mcp-pro      (conseiller)
```

Vous obtenez votre dossier, le moteur de calcul et les parcours guidés. Les
compétences spécialisées, elles, ne sont pas encore publiées sur ChatGPT.

### La première fois

À votre première question, Claude ou ChatGPT vous demandera de vous connecter
à SilverPlan. C'est ce qui relie l'assistant à **votre** dossier : un
particulier ne voit que le sien, un conseiller que son portefeuille.

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

Dans la conversation Claude :

```
/plugin update silverplan
```

(ou `silverplan-pro`.)

Vous ne mettez à jour que les compétences : quelques fichiers de texte. Le
moteur de calcul et votre dossier vivent sur nos serveurs et évoluent de leur
côté, sans que vous ayez quoi que ce soit à faire. Rien à réinstaller, rien à
reconfigurer, et vous ne perdez aucune donnée.

---

Ces plugins sont générés depuis une source unique. Ne les éditez pas à la
main : une modification serait écrasée à la publication suivante.
