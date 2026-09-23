# Public GitHub recipient updates

Repository: https://github.com/rearview-1/smite-private-updates (public).
The new full-folder release is the initial game installation. GitHub hosts a
signed channel plus subsequent changed-file chunks, not a new 42 GiB ZIP for
every change. The historical network installer remains separate; its manifest
and installed-state schemas must not be mixed with this recipient channel.

## Player

1. Extract the new updater-enabled ZIP to a fresh directory and run SETUP.bat.
2. Run PLAY SMITE.bat. It checks the public signed update channel before launch.
3. CHECK FOR UPDATES.bat performs the same check explicitly, without launching.
4. Close the game and wait for ROLLBACK COMPLETE before applying any update.

Players do not need GitHub accounts, GitHub CLI, tokens or extra updater software.
If GitHub is unreachable, startup may use the locally verified installed version.
Signature/hash failures are rejected, not treated as an offline exception.
No account or game authentication data is published. Signing in to the private
game remains separate from downloading public updates.

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
