XPChain Core version 0.17.0-4 is now available:

  <https://github.com/arnoldcho/xpchain-community-core/releases/tag/v0.17.0-4>

This is a maintenance and packaging release focused on build reliability,
multi-OS distribution, and operational documentation updates.

This release does not include any consensus or protocol changes.
It is fully compatible with the current mainnet.

Please report bugs using the issue tracker:

  <https://github.com/arnoldcho/xpchain-community-core/issues>

How to Upgrade
==============

If you are running an older version, shut it down and wait until it has
completely exited. Then install the binaries from this release and restart.

Compatibility
=============

XPChain Core 0.17.0-4 provides release artifacts for:

- Linux x86_64 (tar.gz)
- macOS (dmg, tar.gz)
- Windows x86 / x64 (zip)

Notable changes
===============

Release build and packaging
---------------------------

- Stabilized multi-OS GitHub Actions release workflow.
- Improved packaging outputs for Linux, Windows, and macOS.
- Added SHA-256 checksums for release integrity verification.

macOS build and app packaging improvements
------------------------------------------

- Resolved modern toolchain compatibility issues.
- Improved DMG/app bundle creation flow.
- Enhanced macOS runtime dependency packaging.

Windows/Linux compatibility fixes
---------------------------------

- Applied compatibility fixes for modern compilers and dependencies.
- Improved CI build reliability across platforms.

Project metadata updates
------------------------

- Updated project links and metadata.
- Refreshed About/Splash text to reflect current community maintenance context.

UI text and localization updates
--------------------------------

- Updated About dialog wording to: "This software is under active community
  maintenance and may change between releases."
- Aligned Korean/Japanese translation keys with updated About text.
- Improved Korean wording quality for fee, pruning/reindex, and wallet error
  messages to reduce ambiguity in user-facing dialogs.

Operational documentation
-------------------------

- Added Linux node setup guide and troubleshooting notes.
- Added practical CLI command examples and incident-response references.

XPChain 0.17.0-4 change log
---------------------------

- Multi-OS release automation improvements
- Packaging and runtime dependency fixes
- macOS DMG/app bundle generation improvements
- Windows/Linux compatibility fixes
- About/Splash metadata update
- About wording and localization update (ko/ja)
- Linux node setup documentation

Credits
=======

Thanks to everyone who contributed to this release and verification process.
