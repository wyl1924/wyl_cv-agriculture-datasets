# Privacy transform and verification

Before publication, the frozen 29,878
JPEGs were copied into release TAR assets under pseudonymous, randomly salted
HMAC filenames. The salt and source-to-public mapping stay only in a local
private output outside the public package and Git worktree.
Original filenames, source paths, exact capture groups, capture times, district,
subcounty, GPS values, device fields, comments, thumbnails, XMP, IPTC, and other
nonessential JPEG APP metadata are not published.

Transform: `lossless_jpeg_metadata_strip_preserve_orientation_v2`.

- Only zero-thumbnail standard JFIF, three allowlisted standard sRGB/Display-P3
  ICC profiles, and structurally valid Adobe color-transform markers may be
  retained. ICC profiles contain standard Google/Apple profile copyright text,
  not capture-device identity.
- All original EXIF is removed. A new minimal EXIF block stores only valid
  Orientation values 2-8. The 1,542 invalid source values of 0 were
  normalized to 1 (no rotation).
- Metadata markers are inspected across every JPEG scan, not only before the
  first Start-of-Scan marker. Output ends exactly at the first End-of-Image.
  Trailing data was removed from 5 images (1,922,379
  bytes total), including appended secondary MPO/JPEG frames.
- JPEG coding tables, frame markers, scan headers, and entropy-coded bytes are
  byte-identical through the first image before and after the transform for
  every image; only metadata and post-EOI data are omitted.
- Every one of the 10,911 byte-changed JPEGs was fully decoded before and
  after; raw mode/dimensions/pixels and displayed pixels after EXIF Orientation
  were identical.
- The source scan observed 940 selected images with a GPS IFD. No GPS IFD is
  present in any published JPEG.
- Public manifests contain only published-file hashes; source hashes, paths,
  exact group strings, and the HMAC salt are private.

This is de-identification, not irreversible anonymity. Because image pixels and
JPEG coding data are intentionally unchanged, a person may visually recognize a
scene or match it to an upstream public copy and then inspect upstream metadata.
The transform was applied only to publication copies; frozen training images
were not modified during the build, so model evidence and training hashes remain
valid.
