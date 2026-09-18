<p align="center">
  <img src="icon.png" width="120" alt="DigiDev">
</p>

<h1 align="center">DigiDev</h1>

<p align="center">
  A code editor by <a href="https://github.com/digipacket-net">Digipacket</a>,<br>
  built for local PHP and WordPress work — without Docker.
</p>

<p align="center">
  <a href="https://github.com/digipacket-net/digidev-app/releases/latest"><b>Download the latest version</b></a>
</p>

<p align="center">
  <b>English</b> · <a href="README.fr.md">Français</a>
</p>

---

## What it is

A full editor that also knows how to stand up a local development stack and
work inside it. Fill in one form and it installs a WordPress site, creates its
database, and writes its `wp-config.php` against the local server.

It also connects to your hosting, brings a live site down to your machine, and
afterwards sends back only the files you actually changed.

## Install

**You need an Intel Mac running macOS 12 (Monterey) or later.** Apple Silicon
(M1 and later) is not covered yet, and neither is Windows.

1. Download the `.zip` from [the latest release](https://github.com/digipacket-net/digidev-app/releases/latest).
2. Open it, then drag **DigiDev** into your *Applications* folder.
3. **Open Terminal and run this line:**

   ```sh
   xattr -dr com.apple.quarantine /Applications/DigiDev.app
   ```

4. Launch DigiDev normally.

### Why that third step

The application is not signed by Apple. Without this command macOS says
*"DigiDev is damaged and can't be opened"* — a misleading message: the
application is not damaged, it is simply unknown to Apple, which costs $99 a
year to change.

The command removes the flag macOS attaches to anything downloaded from the
internet. It does not modify the application and it does not turn off any
system protection.

Only run it on a file whose origin you know — here, this repository's Releases
page.

## First steps

### Stand up a WordPress site

Click **Project Launcher** in the side bar, pick the *WordPress* recipe, fill in
the form. DigiDev creates the folder, creates the database, and writes
`wp-config.php` against the local server.

**DigiDev does not install PHP or MySQL.** It finds what is already on your
machine — DBngin, Herd, MAMP, XAMPP, Homebrew — and runs *its own* instance, on
*its own* ports, against *its own* data directory. Your existing installation is
never touched and never reconfigured.

If you have none of those, install [DBngin](https://dbngin.com) first — it is
the simplest, and free.

Then right-click the site: **Start the local server**, then **Open the site in a
browser**.

Deleting a site deletes its database too. Nothing about it is irreversible: the
database is dumped into the site folder first, the folder goes to the Trash, and
only then is the database dropped.

### Work on a site that is already live

Open the **Hosting** panel, then **Add Hosting Account** — FTP or SFTP.

Your credentials are encrypted by the macOS keychain. They are **never** written
in clear text into settings files, so they can never be pushed to a repository
by accident.

Once connected:

| Command | What it does |
| --- | --- |
| **Import the Site Locally** | brings the site down into a folder of your choosing |
| **Deploy Changed Files** | sends back **only** what you changed |
| **Deploy This File** | sends back the open file |
| **Deploy Every File** | sends everything, no comparison |

The first deploy after an import sends nothing: DigiDev recorded what it brought
down, and compares file contents rather than timestamps. Change one file, and
that file — only that file — is what goes back up.

### Add extensions

Two routes, and neither goes through a marketplace.

**The list in the Extensions panel** offers a curated set taken from
[Open VSX](https://open-vsx.org). Every download is checked against the `sha256`
the registry publishes; if it does not match, the file is deleted instead of
installed.

**A `.vsix` file** of your own: `Extensions: Install from VSIX…` from the
command palette (`⇧⌘P`).

### Already included

* **Claude Code** — Anthropic's official extension, unmodified. It needs the
  `claude` CLI installed and signed in on your machine.
* **PHP Debug** (`xdebug.php-debug`) — so *Run and Debug* has an answer on a PHP
  file.

## Updating

There is no automatic update yet. Download the new version, replace the
application in *Applications*, and run the `xattr` command again.

Your settings, extensions and sites live outside the application — in
`~/.digidev` — and survive the replacement.

## What DigiDev does not do

* **No marketplace.** DigiDev defines no extension gallery and never contacts
  Microsoft's.
* **No Copilot.** Removed from the product.
* **No telemetry to Microsoft.**

## Reporting a problem

[Open an issue](https://github.com/digipacket-net/digidev-app/issues) with your
macOS version and your DigiDev version (*DigiDev → About*).

## Licence

DigiDev is a fork of [Code - OSS](https://github.com/microsoft/vscode), which
Microsoft publishes under the MIT licence, and it keeps that licence.

It is **not** Visual Studio Code, and this project is not affiliated with,
endorsed by, or supported by Microsoft.

Copyright (c) 2015 - present Microsoft Corporation — for the Code - OSS source.
Copyright (c) 2026 Digipacket — for the changes.

Licensed under [MIT](LICENSE.txt).
