# Private GitHub recipient updates

Repository: https://github.com/rearview-1/smite-private-updates (private).
The new full-folder release is the initial game installation. GitHub hosts a
signed channel plus subsequent changed-file chunks, not a new 42 GiB ZIP for
every change. The historical network installer remains separate; its manifest
and installed-state schemas must not be mixed with this recipient channel.

## Player

1. Extract the new updater-enabled ZIP to a fresh directory and run SETUP.bat.
2. Obtain access to the private repository using your own GitHub account.
3. Run SIGN IN FOR UPDATES.bat once and complete the GitHub browser sign-in.
4. Close the game and wait for ROLLBACK COMPLETE. Run CHECK FOR UPDATES.bat.
5. After UPDATE CHECK COMPLETE, use PLAY SMITE.bat normally.

GitHub CLI 2.91.0 is bundled with its MIT license. The reviewed Windows executable
has a valid Authenticode signature and SHA256
619787d8ee760105ccf8a554d164c6e67196d1ec77a5fd31c39afe32cff640a9.
Its credential store is local to the player; no token or private game credential
is shipped. Signing in to GitHub does not create a private game account.
Local play never requires checking GitHub first. Updates are explicit.

## Operator

Build a new signed recipient version and complete validate_friend_stage first.
Then run from the project directory:

    powershell.exe -NoProfile -ExecutionPolicy Bypass -File scripts/Publish-GitHubUpdate.ps1 -ReleasePath "releases/SMITE-Private-VERSION"

The publisher authenticates the previous channel and recipient manifest, checks
all new managed hashes, uploads only changed files in at most 64 MiB chunks,
and advances the signed testing channel last. It refuses damaged source files,
wrong signing identity, incompatible base, and runtime/recovery-bootstrap changes.
Those infrequent interpreter/bootstrap changes require a new initial ZIP; normal
application/game-content updates are incremental. If a large UPK changes, that
whole changed file is transferred; this is not a binary-diff algorithm.
Keep the operator signing key local and backed up. Never upload it or accounts.
Repository Git history contains documentation/tooling only, never game binaries.

## Integrity and recovery

RSA/SHA256 purposes separate channel, update recipe and recipient manifests.
Every downloaded chunk and reconstructed file is hash checked before mutation.
Only managed inventory paths are changed. User profiles/accounts, certificates,
captures and active transaction records are excluded. A complete backup journal
precedes mutations; interruption restores the preceding bytes and manifest.
The small recovery bootstrap and bundled interpreter cannot be replaced through
this updater, ensuring recovery remains available after a partial update.

Online REPAIR is not implemented: REPAIR INSTALL retains its matching adjacent
original ZIP behavior. Update rollback preserves the prior changed files locally.
Unchanged missing files still require the original installation media. Download
cache is bounded by individual chunks; rollback backups consume disk space.

## Acceptance

Synthetic rollback/content tests are distinct from signed live GitHub channel
verification and native game acceptance. See CURRENT_STATUS for actual results.
0.3.1 has no update integration and requires the new initial ZIP once. AWS's
existing signed host snapshot is not silently rewritten by publishing a channel.
