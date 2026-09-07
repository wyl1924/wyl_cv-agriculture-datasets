# Restore and verify

1. Download every asset from GitHub Release `agriculture-v2-research-datasets-2026-09-07` into an
   `assets/` directory beside this file.
2. Verify bytes from this directory:

   ```bash
   shasum -a 256 -c SHA256SUMS
   ```

3. List and extract each independent TAR part from the repository root:

   ```bash
   for archive in assets/*.tar; do tar -tf "$archive" >/dev/null; done
   for archive in assets/*.tar; do tar -xf "$archive"; done
   ```

4. Confirm per-image hashes with each `datasets/*/manifest.csv`. Detection
   labels share the pseudonymous image stem. Run detector training from the
   repository root so the relative `path:` in `data.yaml` resolves correctly.

Never treat extraction success alone as integrity verification.
`release-assets.json` is the immutable local expected inventory; it does not
claim upload completion. Before deleting any local training image, create a
separate remote-verification receipt that records every GitHub asset ID, URL,
remote size/digest, downloaded size/SHA-256, recovery-test result, and an overall
`remote_verified` status.
