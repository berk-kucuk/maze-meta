# maze-meta

The Maze Linux metapackage. It depends on every package that makes up a
default Maze system — configuration, branding, the Secure Boot and snapshot
machinery, the recovery kernel (`linux-lts`) and the Maze desktop apps — so a
single `pacman -Syu` brings every Maze machine to the current default set.

Adding a package to the default Maze system means adding it to `depends` here
and bumping `pkgrel`. Publish every package it depends on to `[mazelinux]`
**before** publishing a new `maze-meta`, or `pacman -Syu` fails with
"target not found" on every existing machine.

## Installation

> **Part of Maze Linux.** Every Maze Linux system already has it (pulled in by `maze-meta`). It is built around Maze's own system layout, so installing it on another distribution is not supported.

### From the Maze repository

**On Maze Linux** the repository is already configured:

```bash
sudo pacman -S maze-meta
```

**On Arch Linux and Arch-based distributions**, add the repository once:

1. Import and trust the Maze signing key:

   ```bash
   curl -O https://mazerepo.berkkucukk.com.tr/packages/mazelinux.gpg
   gpg --show-keys --with-fingerprint mazelinux.gpg
   sudo pacman-key --add mazelinux.gpg
   sudo pacman-key --lsign-key 7C4D515A6B930CB04794CEF6147C8159B3E2EE5F
   ```

   The fingerprint `gpg` prints must be `7C4D 515A 6B93 0CB0 4794  CEF6 147C 8159 B3E2 EE5F`.

2. Add the repository to the end of `/etc/pacman.conf`:

   ```ini
   [mazelinux]
   SigLevel = Required DatabaseOptional
   Server = https://mazerepo.berkkucukk.com.tr/packages
   ```

3. Sync and install:

   ```bash
   sudo pacman -Syu maze-meta
   ```

Optionally install `mazelinux-keyring` as well; it keeps the signing key up to date through pacman.

Remove with `sudo pacman -Rns maze-meta`.

### Build from source

```bash
sudo pacman -S --needed base-devel git
git clone https://github.com/berk-kucuk/maze-meta.git
cd maze-meta
makepkg -si
```

## License

Copyright © 2026 Berk Küçük

Released under the GNU General Public License v3.0 — see [LICENSE](LICENSE).
