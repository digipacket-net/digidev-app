<p align="center">
  <img src="icon.png" width="120" alt="DigiDev">
</p>

<h1 align="center">DigiDev</h1>

<p align="center">
  Un éditeur de code par <a href="https://github.com/digipacket-net">Digipacket</a>,<br>
  fait pour travailler en PHP et WordPress en local — sans Docker.
</p>

<p align="center">
  <a href="https://github.com/digipacket-net/digidev-app/releases/latest"><b>Télécharger la dernière version</b></a>
</p>

<p align="center">
  <a href="README.md">English</a> · <b>Français</b>
</p>

---

## Ce que c'est

Un éditeur complet qui sait, en plus, monter une pile de développement locale et
s'y connecter. Vous remplissez un formulaire, il installe WordPress, Laravel,
Symfony ou un serveur Node, crée la base de données et écrit la configuration
contre le serveur local.

Il sait aussi se connecter à votre hébergement, rapatrier un site chez vous,
et ne renvoyer ensuite que les fichiers que vous avez modifiés.

## Installer

**Il faut un Mac Intel et macOS 12 (Monterey) ou plus récent.** Les Mac Apple
Silicon (M1 et suivants) ne sont pas encore couverts, et Windows non plus.

1. Téléchargez le `.zip` depuis [la dernière version](https://github.com/digipacket-net/digidev-app/releases/latest).
2. Double-cliquez dessus, puis glissez **DigiDev** dans votre dossier
   *Applications*.
3. **Ouvrez le Terminal et lancez cette ligne :**

   ```sh
   xattr -dr com.apple.quarantine /Applications/DigiDev.app
   ```

4. Lancez DigiDev normalement.

### Pourquoi cette troisième étape

L'application n'est pas signée par Apple. Sans cette commande, macOS affiche
*« DigiDev est endommagé et ne peut pas être ouvert »* — un message trompeur :
l'application n'est pas endommagée, elle est simplement inconnue d'Apple, ce qui
coûte 99 $ par an à changer.

La commande retire le drapeau que macOS pose sur tout fichier venu d'Internet.
Elle ne modifie pas l'application et ne désactive aucune protection du système.

Ne la lancez que sur un fichier dont vous savez d'où il vient — ici, la page
Releases de ce dépôt.

## Premiers pas

### Monter un site

Cliquez sur **Project Launcher** dans la barre latérale, choisissez une recette,
remplissez le formulaire.

| Recette | Ce que vous obtenez | Ce qu'il faut avoir installé |
| --- | --- | --- |
| **WordPress** | La dernière version, sa base, et le `wp-config.php` écrit contre le serveur local | PHP 7.4 ou plus récent |
| **Laravel** | Une application Laravel neuve, `.env` écrit, clé générée, premières migrations passées | PHP 8.2 ou plus récent, [Composer](https://getcomposer.org) |
| **Symfony** | Une application Symfony neuve, `.env.local` écrit, avec ou sans le pack web complet | PHP 8.2 ou plus récent, [Composer](https://getcomposer.org) |
| **Node starter** | Un petit serveur Express, en JavaScript ou TypeScript, dépendances installées | [Node.js](https://nodejs.org) 20.6 ou plus récent |

DigiDev ne vous demande jamais de taper des identifiants de base dans un fichier
de configuration : il écrit ce qu'il a réellement créé, donc rien n'est périmé
le jour où le serveur change de port.

Les recettes PHP envoient le courrier nulle part — Laravel vers son journal,
Symfony vers un expéditeur vide. Une copie locale d'un site ne doit pas pouvoir
envoyer une réinitialisation de mot de passe à un vrai client par accident.

**PHP et MySQL ne sont pas installés par DigiDev.** Il cherche ce que vous avez
déjà sur la machine — DBngin, Herd, MAMP, XAMPP, Homebrew — et lance *sa propre*
instance, sur *ses propres* ports, avec *son propre* dossier de données. Votre
installation existante n'est jamais touchée, jamais reconfigurée.

Si vous n'avez rien de tout cela, installez d'abord
[DBngin](https://dbngin.com) — c'est le plus simple, et gratuit.

Ensuite, clic droit sur le site : **Start the local server**, puis **Open the
site in a browser**.

Supprimer un site supprime aussi sa base. Rien n'est irréversible : la base est
d'abord exportée dans le dossier du site, le dossier part à la Corbeille, et la
base n'est supprimée qu'après.

### Travailler sur un site déjà en ligne

Ouvrez le panneau **Hosting**, puis **Add Hosting Account** — FTP ou SFTP.

Vos identifiants sont chiffrés par le trousseau de macOS. Ils ne sont **jamais**
écrits en clair dans les fichiers de réglages, donc jamais poussés par erreur
dans un dépôt.

Une fois connecté :

| Commande | Ce qu'elle fait | Où la trouver |
| --- | --- | --- |
| **Import the Site Locally** | rapatrie le site dans un dossier chez vous | panneau Hosting |
| **Deploy Changed Files** | renvoie **seulement** ce que vous avez modifié | le bouton en bas à droite, ou clic droit sur le dossier du projet |
| **Deploy This File** | renvoie le fichier ouvert | l'onglet du fichier, ou clic droit dessus |
| **Deploy Every File** | renvoie tout, sans distinction | clic droit sur le dossier du projet |

Dès que vous êtes connecté, un bouton apparaît **en bas à droite** avec le nom
de votre compte d'hébergement. Modifiez vos fichiers, cliquez dessus, et DigiDev
vous dit ce qu'il s'apprête à envoyer avant d'envoyer quoi que ce soit.

#### Un dossier que vous aviez déjà

Si le dossier local ne vient pas de **Import the Site Locally**, DigiDev ignore
où il se place sur le serveur — il enverrait vos fichiers là où le serveur vous
dépose à la connexion, souvent un niveau au-dessus du site.

Dites-le-lui une fois :

1. Ouvrez votre dossier local et connectez-vous au compte.
2. Dans **Remote files**, naviguez jusqu'au dossier du site — celui qui contient
   `index.php` ou `wp-content`.
3. Cliquez l'icône **lien** à côté : *Link This Folder to the Site*.

Ensuite, le bouton de déploiement envoie là. Rien n'est téléchargé et rien
n'est touché sur le serveur au moment où vous liez.

Le **premier** envoi après le lien transfère **tous** les fichiers, pas seulement
ceux que vous avez modifiés. DigiDev n'a pas vu ce qu'il y a sur le serveur et
ne supposera pas que votre copie lui correspond — le supposer reviendrait à
sauter en silence les fichiers qui diffèrent vraiment. Les envois suivants sont
incrémentaux.

#### Envoyer à chaque enregistrement

Activez **`digidev.hosting.deployOnSave`** dans les réglages et chaque
enregistrement part directement sur le serveur.

Ça ne marche que sur un dossier lié, et c'est désactivé par défaut pour une
raison : ça écrit sur un site en production sans confirmation. Laissez-le
désactivé tant que vous travaillez sur un site qui reçoit de vrais visiteurs.

Le premier envoi après un import ne renvoie rien : DigiDev sait ce qu'il a
rapatrié, et compare le contenu réel des fichiers, pas leur date. Modifiez un
fichier, et c'est celui-là — seulement celui-là — qui part.

**Logs serveur** est la troisième vue de ce panneau. Quand un transfert échoue,
la raison est en haut — la ligne la plus récente d'abord. Votre mot de passe n'y
apparaît jamais, même quand un serveur vous renvoie votre échec de connexion.

### Laisser un agent travailler sur le projet

**AI Agents**, dans la barre d'activité, applique une compétence spécialisée au
projet ouvert et vous montre ce qu'il veut changer avant que rien ne change.

1. Cliquez un agent — **SEO Agent** ou **Security Agent** pour commencer.
2. La première fois, DigiDev demande quel assistant fera le travail : Claude
   Code, OpenAI Codex ou Gemini CLI. Il doit être installé et connecté sur
   votre Mac ; sinon DigiDev ouvre la page d'installation ou un terminal avec
   la commande de connexion. **DigiDev ne demande jamais de clé et n'en
   conserve aucune** — l'outil de l'assistant garde sa propre session.
3. L'agent travaille sur une **copie** de votre projet. Vos fichiers ne sont
   pas sur son chemin.
4. Quand il termine, son rapport s'ouvre à côté de l'éditeur et **Proposed
   changes** liste chaque fichier qu'il veut modifier. Cliquez-en un pour voir
   la différence ; **Apply** ou **Discard** chacun, ou tous d'un coup.

Le Security Agent analyse, rapporte par gravité, et **demande la permission**
avant de corriger quoi que ce soit. Répondez avec **Reply to the Agent** — il
poursuit la même conversation sur la même copie, et c'est seulement alors qu'il
y a une différence à examiner.

Vos propres agents vont dans `~/.digidev/agents/<nom>/` : un `SKILL.md` et, si
vous voulez un titre ou une icône, un `agent.json`.

### Partager un skill avec tous les assistants

Un **skill** est un dossier d'instructions qu'un assistant IA lit avant
d'effectuer un travail précis — relire un thème, écrire une migration, suivre
vos conventions maison. Claude Code les appelle des skills ; Codex et Gemini
n'ont pas cette notion et lisent un seul fichier à la racine du projet.

**Project Launcher → Skills** efface cette différence.

1. **Import a Skill** — désignez un dossier ou un `.zip`. Il rejoint votre
   bibliothèque dans `~/.digidev/skills/`, accessible depuis tous vos projets.
2. **Apply to This Project** — choisissez quels assistants doivent le voir. Le
   skill est écrit **une seule fois** dans `.claude/skills/<nom>/`, et ceux qui
   ne savent pas lire un dossier de skill sont pointés vers cette copie depuis
   `AGENTS.md` et `GEMINI.md`.
3. **Make Available in Every Project** — le copie dans `~/.claude/skills/`, là
   où Claude Code cherche les skills valables partout.

Ce que vous avez écrit à la main dans `AGENTS.md` ou `GEMINI.md` n'est jamais
touché. DigiDev ne réécrit que ce qui se trouve entre ses deux commentaires
repères : appliquer un second skill met ce bloc à jour au lieu d'en ajouter un
autre, et retirer le dernier skill emporte le bloc avec lui.

Un skill sans `description` dans son `SKILL.md` est refusé. Sans elle, un
assistant n'a aucun moyen de savoir quand l'utiliser — il paraîtrait installé
et ne ferait rien.

### Ajouter des extensions

Deux chemins, et aucun ne passe par une place de marché.

**La liste dans le panneau Extensions** propose des extensions choisies, prises
sur [Open VSX](https://open-vsx.org), regroupées pour qu'on y trouve ce qu'on
cherche :

| Groupe | Ce qu'il contient |
| --- | --- |
| **AI** | ChatGPT, Gemini Code Assist |
| **PHP** | Intelephense, DocBlocker, résolveur d'espaces de noms |
| **Laravel** | Syntaxe Blade, IntelliSense supplémentaire |
| **Web** | Prettier, ESLint, Tailwind, renommage de balise, Live Server |
| **Tools** | GitLens, Error Lens, EditorConfig, Path IntelliSense, dotenv, YAML, correcteur orthographique |

Chacune s'installe et se désinstalle depuis cette liste — sans compte de place
de marché, sans `.vsix` à chercher. Chaque téléchargement est comparé à
l'empreinte `sha256` publiée par le registre ; si elle ne correspond pas, le
fichier est supprimé au lieu d'être installé.

Pour ajouter les vôtres, créez `~/.digidev/extensions.json` :

```json
{ "extensions": [{ "id": "publisher.name", "group": "Mine", "note": "pourquoi" }] }
```

**Un fichier `.vsix`** que vous avez vous-même : `Extensions: Install from
VSIX…` depuis la palette de commandes (`⇧⌘P`).

### Déjà inclus

* **Claude Code** — l'extension officielle d'Anthropic, non modifiée. Il faut
  que le CLI `claude` soit installé et connecté sur la machine.
* **PHP Debug** (`xdebug.php-debug`) — pour que *Exécuter et déboguer* ait une
  réponse sur un fichier PHP.

## Mettre à jour

Il n'y a pas encore de mise à jour automatique. Téléchargez la nouvelle version,
remplacez l'application dans *Applications*, et relancez la commande `xattr`.

Vos réglages, extensions et sites vivent en dehors de l'application — dans
`~/.digidev` — et survivent au remplacement.

## Ce que DigiDev ne fait pas

* **Aucune place de marché.** DigiDev ne définit pas de galerie d'extensions et
  ne contacte jamais celle de Microsoft.
* **Aucun Copilot.** Retiré du produit.
* **Aucune télémétrie vers Microsoft.**

## Signaler un problème

[Ouvrez un ticket](https://github.com/digipacket-net/digidev-app/issues) en
indiquant votre version de macOS et le numéro de version de DigiDev
(*DigiDev → À propos*).

## Licence

DigiDev est un fork de [Code - OSS](https://github.com/microsoft/vscode), que
Microsoft publie sous licence MIT, et il conserve cette licence.

Ce n'est **pas** Visual Studio Code, et ce projet n'est ni affilié à Microsoft,
ni approuvé ni soutenu par Microsoft.

Copyright (c) 2015 - present Microsoft Corporation — pour la source Code - OSS.
Copyright (c) 2026 Digipacket — pour les modifications.

Sous licence [MIT](LICENSE.txt).
