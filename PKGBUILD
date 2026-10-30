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
pkgver=1.9.0
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
  # The app store: browses [mazelinux] and runs installs in a terminal behind
  # `sudo -k`, so it holds no privilege of its own. Its user timer checks for
  # Maze app updates every 6 hours — one ~15 KiB fetch from the Maze repo,
  # nothing else leaves the machine — and can be switched off in the app.
  'maze-store'
  # The official donation addresses, always one click away in the menu. Shows
  # an address only after gpgv has verified the signed list against the Maze
  # package key; it touches the network only when the user asks it to check
  # for new addresses. No service, no timer, no privilege.
  'maze-donate'
  # Separate encrypted spaces for files and folders, on gocryptfs through FUSE
  # as the user — no root, no network. Its only background piece is a user
  # service that does nothing until logout, then locks every open capsule.
  'maze-capsule'
  # Password manager: a Bitwarden-compatible CLIENT for the user's own
  # Vaultwarden (or a vault kept only on this computer). Everything is
  # encrypted locally before it goes anywhere; it contacts only the server
  # the user signs in to. No service, no timer, no telemetry.
  'maze-vault'
  # AI Usage widget: plan limits for coding agents (Claude Code / Desktop,
  # Codex, Gemini CLI, Copilot, OpenCode). INSTALLED, but deliberately NOT
  # placed on the panel by maze-plasma-config: most Maze users are not
  # developers, so it only appears in "Add Widgets…" for those who want it.
  # It contacts a provider only through that tool's own existing login; with
  # nothing signed in it reads local files and stays offline.
  'plasma6-applets-ai-usage'
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
  # No -headers here any more. NVIDIA comes prebuilt from Arch (nvidia-open /
  # nvidia-open-lts) — maze-gpu-driver installs headers itself on the DKMS path
  # it still uses for non-Arch kernels — and the installer keeps
  # broadcom-wl-dkms, marking both header packages explicit, only on machines
  # with Broadcom wireless. Depending on them here made every machine download
  # and keep ~60 MB of LTS headers per kernel update for nothing.
  'linux-lts'
  # ── Gaming ─────────────────────────────────────────────────────────────
  # Fast Steam shader pre-compilation, bigger shader caches, GameMode with a
  # sched_ext gaming scheduler, ntsync, MangoHud, gamescope. No global security
  # relaxation: anything that trades security for speed is scoped to a running
  # game. Does NOT pull in Steam itself (the ISO lists it).
  'maze-gaming'
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
