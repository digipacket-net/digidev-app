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

| Commande | Ce qu'elle fait |
| --- | --- |
| **Import the Site Locally** | rapatrie le site dans un dossier chez vous |
| **Deploy Changed Files** | renvoie **seulement** ce que vous avez modifié |
| **Deploy This File** | renvoie le fichier ouvert |
| **Deploy Every File** | renvoie tout, sans distinction |

Le premier envoi après un import ne renvoie rien : DigiDev sait ce qu'il a
rapatrié, et compare le contenu réel des fichiers, pas leur date. Modifiez un
fichier, et c'est celui-là — seulement celui-là — qui part.

**Logs serveur** est la troisième vue de ce panneau. Quand un transfert échoue,
la raison est en haut — la ligne la plus récente d'abord. Votre mot de passe n'y
apparaît jamais, même quand un serveur vous renvoie votre échec de connexion.

### Ajouter des extensions

Deux chemins, et aucun ne passe par une place de marché.

**La liste dans le panneau Extensions** propose des extensions choisies, prises
sur [Open VSX](https://open-vsx.org). Chaque téléchargement est comparé à
l'empreinte `sha256` publiée par le registre ; si elle ne correspond pas, le
fichier est supprimé au lieu d'être installé.

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
