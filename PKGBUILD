# Maintainer: Berk Küçük <dev.berkkucukk@gmail.com>
#
# maze-meta — the single source of truth for "what is a Maze Linux system".
#
# This is a pure metapackage: it ships NO files, it only `depends` on every
# package that defines the Maze desktop (its own maze-* config/branding/apps
# plus a few curated third-party tools like firejail). Installing it pulls the
# whole set in; pacman skips anything already present.
#
# Why it exists — pushing new defaults to ALREADY-INSTALLED systems:
#   `pacman -Syu` only updates installed packages and pulls their NEW deps. A
#   brand-new standalone package is never auto-installed. So to add a package to
#   every existing Maze machine, add it to THIS file's depends and bump pkgrel:
#   on the next `pacman -Syu`, maze-meta updates and pacman installs the new
#   dependency automatically. One place to manage every default package.
#
# Delivery:
#   * New ISOs: list `maze-meta` in packages.x86_64 (it pulls the rest).
#   * Existing systems: they must already HAVE maze-meta for the update to reach
#     them — bootstrap it once by making an always-installed package (maze-tools)
#     depend on maze-meta. After that, editing this depends list is enough.
#
# NOTE: maze-installer is intentionally NOT listed — it is the live-ISO-only
# Calamares installer and must never land on an installed desktop.

pkgname=maze-meta
pkgver=1.5.0
pkgrel=3
pkgdesc="Maze Linux metapackage — pulls in every default Maze package (config, branding, apps, security tooling)"
arch=('any')
url="https://mazelinux.berkkucukk.com.tr"
license=('GPL3')
depends=(
  # ── Maze configuration & branding ──────────────────────────────────────
  'maze-branding'
  'maze-hardening'
  'maze-plasma-config'
  # Listed here ON PURPOSE. This is the one subsystem whose failure mode is
  # "the machine does not boot", and a maze-meta dependency is what gives
  # ALREADY-INSTALLED machines an update path for it (they were shipped the
  # same scripts as unowned files by the installer; the package takes over).
  'maze-secureboot'
  # Automatic btrfs snapshots around every pacman transaction. Covers the half
  # maze-secureboot does not: a bad library or a half-applied upgrade leaves a
  # running system unusable without ever touching the boot chain.
  'maze-snapshots'
  'maze-tools'
  'mazelinux-keyring'
  # ── Maze applications ──────────────────────────────────────────────────
  'maze-guard'        # network security monitor (MITM / MAC / firewall)
  'entropy-shield'
  'qlam'
  'hazedrop'
  'haze'
  'maze-ai'           # local models via Ollama — nothing leaves the machine
  'maze-connect'
  'maze-cloak'
  # NOT listed, on purpose: linux-chan-ai and sentinai.
  #
  # Both talk to Google Gemini. Linux Chan has no offline mode at all, and it
  # reads files and screenshots for you — everything it sees goes to Google.
  # SentinAI now prefers a local Ollama backend, but the cloud path is still
  # there, and its PassGen/OSINT tooling is aimed at authorised penetration
  # testing rather than at the everyday desktop this metapackage defines.
  #
  # A distribution whose promise is that nothing leaves the machine by default
  # cannot install either of them without being asked. They stay in the
  # [mazelinux] repo and remain one `pacman -S` away for anyone who wants them.
  # Both now show a notice the first time the cloud backend is used.
  # ── Recovery kernel ────────────────────────────────────────────────────
  # A SECOND, independent kernel, kept permanently. With one kernel installed, a
  # bad update is a live-USB recovery; with two, the previous known-good image is
  # already built and signed on the ESP. maze-sb-sign keeps mainline as the boot
  # default (it picks the highest version) and leaves every installed kernel's
  # UKI in place, so this costs one extra image on the ESP and nothing else.
  # -headers is required: nvidia-open-dkms and broadcom-wl-dkms have to build
  # against LTS too, or the recovery kernel comes up without graphics or wifi.
  'linux-lts'
  'linux-lts-headers'
  # ── Curated third-party security tooling ───────────────────────────────
  'firejail'          # application sandbox
  # ── Updates ────────────────────────────────────────────────────────────
  # paru, from [mazelinux]. Maze's own update instructions (the installer's
  # summary, maze-doctor) say `paru -Syu`, because several default desktop
  # apps come from the AUR and pacman alone never updates them. A machine
  # without paru cannot follow that — and machines installed from ISOs that
  # predate paru being in the repo may not have it. As a dependency here every
  # Maze machine gets it, and gets it updated by pacman from now on.
  'paru'
  # NOT listed: said360. It is a decorative Plasma widget, not a security
  # tool, and not part of the default Maze desktop. It stays in [mazelinux]
  # for anyone who installs it by hand; dropping it here leaves it on machines
  # that already have it (it simply becomes an orphan dependency).
  )
source=()

# Metapackage: no payload. package() must exist, but installs nothing.
package() {
  :
}
