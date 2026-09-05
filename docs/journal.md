# Journal — dépôt `rnab26/melissa-nabet-site`

Ce fichier n'existe que dans ce dépôt-ci. Le journal de fond du projet est
`PROJECT_LOG.md` dans le dépôt du CRM (`rnab26/melissa-nabet`).

---

## 2026-09-04 — Ce qu'est ce dépôt : un miroir de déploiement, pas un dépôt de travail

**Conclusion : ne rien développer ici.** Ce dépôt n'est pas abandonné — il est en
ligne et il sert — mais ce n'est pas là que le code du site s'écrit. Toute
modification faite ici serait écrasée à la prochaine copie depuis le CRM, sans
que personne le remarque.

### Les deux dépôts, et ce qui les distingue

| | `rnab26/melissa-nabet` (CRM) | `rnab26/melissa-nabet-site` (ici) |
|---|---|---|
| Rôle | Application de gestion + **source** du site vitrine | **Copie servie** du site vitrine |
| Contenu | `index.html` de 465 Ko (CRM), `site-vitrine/`, `tests/`, `supabase/`, `PROJECT_LOG.md`, `CLAUDE.md` | `index.html` (11 Ko), `README.md`, le workflow Pages |
| Adresse servie | https://rnab26.github.io/Melissa-Nabet/ (connexion obligatoire) | https://rnab26.github.io/melissa-nabet-site/ (public) |
| Activité | **actif** — dernier commit le 04/09 à 15h35 UTC, une autre session y travaille | 2 commits, tous du 04/09 matin, aucun développement propre |
| Galerie photos, import, retouche fal.ai | **c'est là que ça vit** | absent, et n'a pas vocation à y être |

### Vérifié, pas déduit

- `diff site-vitrine/index.html` (dépôt CRM) contre `index.html` (ici) : **identiques
  octet pour octet**. Idem pour `README.md` et `.github/workflows/pages.yml`.
  Ce dépôt est une copie exacte du dossier `site-vitrine/` du CRM.
- Le `README.md` d'ici le dit lui-même : « Ce dossier est la source d'un dépôt
  distinct : `rnab26/melissa-nabet-site` […]. Il est gardé ici en attendant. »
  La source est donc le CRM ; ce dépôt est la destination.
- Le workflow Pages du CRM contient une étape `rm -rf site-vitrine` pour ne pas
  servir le site vitrine sur le domaine du CRM. Le dossier vit toujours là-bas.
- Le site est **en ligne et alimenté** : `GET https://rnab26.github.io/melissa-nabet-site/`
  → HTTP 200, 11 031 octets, identiques au dépôt. Dernier déploiement Pages :
  succès (run 33853953453, commit `029070a`).
- Le manifeste public répond HTTP 200 et contient **1 réalisation publiée**
  (« Bureau Sébastien », 2026, 5 photos), publiée le 04/09 à 10h05.
  Les photos se chargent : `p0.jpg` 447 Ko, `t0.jpg` 106 Ko, `p4.jpg` 421 Ko, tous HTTP 200.
  *(Le `PROJECT_LOG.md` du CRM dit encore « aucune réalisation publiée » — c'est périmé,
  ça a changé depuis.)*
- Aucune issue ouverte, aucune pull request, une seule branche (`main`).

### Pourquoi je m'arrête là, plutôt que de développer

1. **La priorité annoncée — la galerie de photos (import multiple, miniatures,
   réordonner, légender, sélection multiple, retouche IA via fal.ai/rafale) —
   n'existe pas dans ce dépôt et ne doit pas y exister.** Elle est dans le CRM,
   côté administration, derrière une connexion. Ce dépôt-ci ne contient que la
   page publique en lecture seule, qui affiche ce que le CRM a publié.
2. **Une autre session travaille sur ce sujet en ce moment même**, dans le CRM :
   commits « Retouche IA : réglages, plafond bloquant, erreurs visibles » (15h35),
   « Comparateur avant/après, historique par photo » (15h10). Développer ici en
   parallèle ferait doublon.
3. **Écrire dans ce dépôt fait diverger le code déployé du code versionné.** Le
   fichier de référence est `site-vitrine/index.html` dans le CRM. Une modification
   faite ici disparaît à la copie suivante.

### Une seule modification faite ici, et pourquoi

Le workflow publie `path: '.'`, c'est-à-dire **tout le dépôt**. Sans garde-fou, ce
journal serait servi publiquement sur le site de Mélissa
(`…/melissa-nabet-site/docs/journal.md`). J'ai donc ajouté une étape
`rm -rf docs` avant l'envoi — exactement le patron déjà en place dans le CRM
(`rm -rf site-vitrine`). C'est la **seule divergence volontaire** entre ce dépôt et
`site-vitrine/` du CRM : si quelqu'un recopie le dossier ici en écrasant tout,
il faut remettre cette étape (et ce fichier disparaîtra).

### Ne pas casser

- **Aucune clé Supabase dans `index.html`**, même « publishable ». La page n'en a
  pas besoin : elle ne lit que du public. C'est une garantie structurelle, pas une
  précaution.
- **`site-vitrine/` du CRM reste la source.** Modifier le site = modifier là-bas,
  puis recopier ici. Ne jamais partir de ce dépôt-ci.
- **L'étape `rm -rf docs`** du workflow, tant que ce journal existe.
- Le déclencheur du workflow (`push` sur `main`) : c'est ce qui redéploie le site.

### Ce qui reste à faire pour le site public

Ces chantiers sont déjà listés dans le tableau de bord du projet
(https://claude.ai/code/artifact/c7ead2fa-509a-4bf4-a2c5-ac18a5063d84, section
« Site vitrine »). Ils touchent presque tous **les deux dépôts à la fois** : un
champ ajouté côté CRM, publié dans le manifeste, puis affiché par la page. Ils ne
peuvent donc pas se faire d'ici seul.

- `si02` Sections et catégories de réalisations, avec filtre visiteur — les deux dépôts.
- `si03` Textes de présentation (lieu, surface, année, description) — les deux dépôts.
- `si04` Page À propos et contact (mailto + WhatsApp, sans serveur) — surtout ici.
- `si05` Référencement et aperçu de partage (titre/description par projet, image
  d'aperçu, plan du site) — **presque entièrement ici**, c'est le seul chantier
  qui pourrait se traiter dans ce dépôt sans toucher au CRM. Aujourd'hui la page
  n'a qu'un `og:title` fixe : un lien partagé sur WhatsApp s'affiche nu.
- `si06` Nom de domaine propre (~12 €/an) — dépense, décision de Raphaël.
- `si07` Compter les visites, sans cookie.

### Ce que j'attends de Raphaël

1. **Trancher où vit le code du site.** Aujourd'hui il vit à deux endroits, et rien
   n'automatise la copie. Deux options propres :
   - *(recommandé)* Le CRM reste la source, et on ajoute un workflow qui pousse
     automatiquement `site-vitrine/` vers ce dépôt à chaque changement. Plus de copie
     manuelle, plus de dérive possible. Demande un jeton avec droit d'écriture sur ce
     dépôt, en secret du dépôt CRM.
   - Ce dépôt devient la source, et `site-vitrine/` est supprimé du CRM.
   Tant que ce n'est pas tranché, les sessions futures retomberont sur la même
   question et risqueront d'écrire du côté qui sera écrasé.
2. **Confirmer que la galerie d'administration se traite bien dans le CRM.** Le
   brief donné à cette session la demandait ici ; elle n'y est pas et n'a pas à y être.
3. `si06` (nom de domaine) : achat, donc décision qui n'appartient qu'à lui.

### État à l'arrêt de cette session

Rien de développé ici, volontairement — voir plus haut. Ajouté : ce journal, et
l'étape `rm -rf docs` du workflow pour ne pas le publier. Le site en ligne est
inchangé côté visiteur : vérifié après déploiement.

---

## 2026-09-04 — Légendes de photos (copie depuis le CRM)

Copie de `site-vitrine/index.html` du dépôt CRM, comme le veut le rôle de miroir
décrit plus haut. **Rien n'a été écrit ici** : le fichier est identique octet pour
octet à sa source (vérifié par `diff` après copie).

**Ce qui change pour le visiteur** : une photo peut porter une légende, écrite depuis
le CRM (fiche d'une réalisation → pied d'une vignette → « Titre et légende »). La
légende s'affiche sous la photo dans la page du projet, reprise en plein écran, et
sert de texte alternatif. Une photo sans légende n'affiche rien du tout — pas de
blanc sous l'image.

Le manifeste porte la légende dans `photos[].caption`. Les manifestes déjà publiés
n'en ont pas : la page les traite comme des photos sans légende, rien à migrer.

Vérifié avant copie, côté CRM : `tests/site.test.mjs`, 22 contrôles, 0 échec, dont
l'affichage de la légende sous la photo, en plein écran, son absence quand il n'y en
a pas, et l'absence de toute clé d'accès dans la page servie.

---

## 2026-09-04, 20h10 UTC — Vérification après coup : le miroir a bien fonctionné

Relance nocturne, rien à développer ici (voir le constat plus haut). Contrôles faits :

- Le constat est bien versionné sur `main` et a servi : la session qui a copié les
  légendes depuis le CRM (`51f52b0`) a suivi le rôle de miroir décrit ici, sans
  écrire de code propre à ce dépôt.
- **L'étape `rm -rf docs` a survécu à cette copie** — c'était le risque signalé plus
  haut. Vérifié sur `origin/main` et en ligne : `…/docs/journal.md` renvoie HTTP 404,
  le journal n'est pas servi au public.
- Déploiements Pages n°2 (`a274e93`) et n°3 (`51f52b0`) : **succès** tous les deux.
- Page publique : HTTP 200, 11 876 octets, identique octet pour octet à `origin/main`.
  Les légendes sont bien en ligne.

Rien d'autre à faire dans ce dépôt tant que la question « où vit le code du site »
n'est pas tranchée par Raphaël (voir plus haut). Les relances suivantes n'auront rien
à y faire non plus.

---

## 2026-09-05 — Textes de présentation des projets (copie depuis le CRM)

Copie de `site-vitrine/index.html` du dépôt CRM, identique octet pour octet à sa
source (vérifié par `diff` après copie). Rien n'a été écrit ici.

**Ce qui change pour le visiteur** : sous le titre d'un projet s'affichent
maintenant l'année, le lieu, la surface et le type de mission quand ils sont
renseignés, puis un texte de présentation. Tous ces champs se remplissent depuis
le CRM (fiche d'une réalisation). Un champ vide ne s'affiche pas du tout — pas
d'étiquette sans valeur, pas de ligne vide.

Sur la liste des projets, la carte porte désormais l'année, le lieu et le type de
mission plutôt qu'un décompte de photos ; s'il n'y a ni lieu ni mission, on
retombe sur le décompte pour ne pas laisser une ligne quasi vide.

Les manifestes déjà publiés n'ont aucun de ces champs : la page les traite comme
absents, rien à migrer.

Vérifié avant copie, côté CRM : `tests/site.test.mjs`, 24 contrôles, 0 échec,
dont l'affichage des informations sous le titre, le texte de présentation, et
toujours l'absence de toute clé d'accès dans la page servie.

---

## 2026-09-05 — Aperçu de partage, référencement, chargement (copie depuis le CRM)

Copie de `site-vitrine/` du dépôt CRM : `index.html` (identique octet pour octet,
vérifié par `diff`), plus deux fichiers nouveaux, `robots.txt` et `sitemap.xml`.

**Ce qui change** : un lien vers le site partagé sur WhatsApp, Instagram ou
LinkedIn affiche désormais une image et une description. Les robots de ces
services ne lisent pas le JavaScript : l'image est donc déclarée en dur dans la
page, à une adresse fixe que **le CRM réécrit à chaque publication** (couverture
de la dernière réalisation publiée) et efface quand plus rien n'est en ligne.

Le titre de l'onglet et la description suivent le projet ouvert, puis reviennent à
ceux du site quand on referme. Adresse canonique, données structurées schema.org,
robots.txt et sitemap.xml ajoutés.

Chargement : les vignettes au-delà des deux premières attendent d'être approchées,
décodage hors du fil principal, priorité haute sur la première photo d'un projet.

Si le chemin de l'image d'aperçu change côté CRM (`shareImagePath`), la balise
`og:image` de cette page doit changer en même temps.

Vérifié avant copie : `tests/site.test.mjs`, 36 contrôles, 0 échec.

---

## 2026-09-05 — Filtre par catégorie (copie depuis le CRM)

Copie de `site-vitrine/index.html` du dépôt CRM, identique octet pour octet.

**Ce qui change pour le visiteur** : une barre de filtres au-dessus de la grille,
avec le décompte par catégorie (« Appartement (4) », « Bureau (2) »…). Elle se
construit à partir des projets réellement publiés — rien à tenir à jour — et ne
s'affiche pas tant qu'il n'y a pas au moins deux catégories. La catégorie se
renseigne depuis le CRM, dans la fiche de la réalisation.

Vérifié avant copie : `tests/site.test.mjs`, 42 contrôles, 0 échec, dont l'ouverture
d'un projet depuis une liste filtrée (le piège classique : ouvrir celui du même rang
dans la liste complète).

---

## 2026-09-05 — À propos et contact (copie depuis le CRM)

Copie de `site-vitrine/index.html` du dépôt CRM, identique octet pour octet.

**Ce qui change pour le visiteur** : une section « À propos » en bas de page, avec
le texte de présentation et les liens pour joindre l'architecte — e-mail, WhatsApp
(numéro converti au format international) et Instagram.

**Rien n'est affiché tant que rien n'est rempli** : chaque lien manquant disparaît,
et si tout est vide la section n'existe pas du tout. Ces informations se saisissent
dans le CRM (onglet Réalisations → « ⚙ Le site public ») puis s'envoient par un
bouton explicite. Aucune coordonnée n'est reprise automatiquement des devis.

L'adresse e-mail n'est pas écrite dans le HTML servi : le lien est fabriqué au
chargement à partir du manifeste. Ça décourage les robots collecteurs ordinaires,
ça ne rend pas l'adresse secrète — le manifeste est public.

Vérifié avant copie : `tests/site.test.mjs`, 49 contrôles, 0 échec.

---

## 2026-09-05, 18h — La recopie devient automatique (la question ouverte est tranchée)

Raphaël a tranché : **le CRM reste la source, la recopie est désormais automatique.**
Il a créé le jeton d'écriture et l'a déposé dans le secret `SITE_VITRINE_TOKEN` du dépôt
du CRM. Le workflow `.github/workflows/sync-site-vitrine.yml` (côté CRM) recopie
`site-vitrine/` ici à chaque changement sur `main`.

**Ce dépôt ne se modifie plus à la main. Jamais.** Toute modification du site se fait
dans `site-vitrine/` du dépôt CRM ; la recopie suivante écraserait ce qui aurait été
écrit ici.

**Deux exceptions, qui appartiennent à ce dépôt et ne sont jamais écrasées :**
- `.github/` — le déploiement Pages d'ici, avec son garde-fou `rm -rf docs`.
- `docs/` — ce journal.

C'est un `rsync --delete` avec ces deux dossiers en exclusion : rsync protège de la
suppression ce qu'il exclut. Le jeton n'a volontairement **pas** le droit d'écrire des
workflows, donc même une erreur de configuration ne peut pas emporter le garde-fou.

**Vérifié en conditions réelles, pas déduit** (première exécution, run 33982469799) :
- Le workflow a poussé ici tout seul : commit `c2e4607` par `github-actions[bot]`.
- `index.html` est identique octet pour octet à `site-vitrine/index.html` du CRM.
- Deux fichiers nouveaux sont bien arrivés : `sitemap.xml` et `robots.txt` (HTTP 200 en ligne).
- `docs/journal.md` a survécu à la recopie, et reste non publié (HTTP 404 en ligne).
- Le garde-fou `rm -rf docs` est toujours dans `.github/workflows/pages.yml`.
- Le site public répond HTTP 200 avec la nouvelle version.

Ce que ça règle : ce dépôt avait pris du retard sur le CRM (catégories, filtre,
référencement, sitemap étaient déjà écrits côté source mais pas recopiés). La première
exécution a rattrapé ce retard toute seule.

**Ne pas casser**
- Ne pas retirer les exclusions `--exclude='.github/'` et `--exclude='docs/'` du workflow
  de recopie : sans elles, le journal serait publié sur le site public et le garde-fou
  sauterait.
- Ne pas travailler dans ce dépôt. La source est `site-vitrine/` du CRM.

**Ce qui reste à surveiller**
- **Le jeton a une date d'expiration.** Le jour où il expire, la recopie s'arrête. Le
  workflow échoue alors avec un message explicite (« Le secret SITE_VITRINE_TOKEN est
  absent ») plutôt qu'en silence — mais il faudra le régénérer et le recoller dans le
  secret du dépôt CRM. Aucune alerte automatique n'est en place pour prévenir avant.
- La branche `claude/constat-depot-miroir`, déjà fusionnée, n'a pas pu être supprimée :
  le proxy git de la session refuse la suppression de branche et le connecteur GitHub
  n'expose pas d'outil pour ça. Sans conséquence, juste pas net.
