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
pkgver=1.1.0
pkgrel=1
pkgdesc="Maze Linux metapackage — pulls in every default Maze package (config, branding, apps, security tooling)"
arch=('any')
url="https://mazelinux.berkkucukk.com.tr"
license=('GPL3')
depends=(
  # ── Maze configuration & branding ──────────────────────────────────────
  'maze-branding'
  'maze-hardening'
  'maze-plasma-config'
  'maze-tools'
  'mazelinux-keyring'
  # ── Maze applications ──────────────────────────────────────────────────
  'maze-guard'        # network security monitor (MITM / MAC / firewall)
  'entropy-shield'
  'qlam'
  'hazedrop'
  'haze'
  'linux-chan-ai'
  'sentinai'
  'maze-ai'
  'maze-connect'
  # ── Curated third-party security tooling ───────────────────────────────
  'firejail'          # application sandbox
)
source=()

# Metapackage: no payload. package() must exist, but installs nothing.
package() {
  :
}
