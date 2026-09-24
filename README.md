# SMITE compatibility updates

Public signed update channel for the full-folder compatibility build.

## Latest update: 0.3.4

Run CHECK FOR UPDATES.bat from an installed 0.3.3 build to install 0.3.4.
This update contains 10 changed code files (100,410 payload bytes, plus signed
metadata); no new full game download is required. [Changes and limitations](docs/release-0.3.4.md).

## Current baseline:0.3.3

Install the separately distributed, validated0.3.3 ZIP once. Existing0.3.2
installations cannot upgrade this particular release incrementally because it
changes protected recovery-launcher/prerequisite files. Preserve your user data;
do not bypass the updater protection. Historical0.3.2 release assets remain.

On0.3.3, CHECK FOR UPDATES.bat checks the signed channel without launching the
game. PLAY SMITE.bat and PLAY ON AWS.bat check before startup. Normal subsequent
application/content releases download only changed files. No GitHub account is
needed. Close SMITE and wait for ROLLBACK COMPLETE before applying updates.

[Player and operator instructions](docs/github-recipient-updates.md)

The game ZIP is distributed separately. AWS enrollment and private game accounts
are also separate; this repository contains neither. Game binaries are never
committed to Git history. Signing keys, private certificates, account databases
and credentials are never published. Native multiplayer acceptance remains
separate from updater/package validation.
