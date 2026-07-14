# UniMol migration package 2026-07-14

This directory contains a split tar.gz archive because GitHub rejects single files larger than 100 MB.

The archive was split into files named `migration_package_20260714.tar.gz.part-*`.

## Restore

Run from this directory:

```bash
sha256sum -c SHA256SUMS
cat migration_package_20260714.tar.gz.part-* > migration_package_20260714.tar.gz
sha256sum -c ARCHIVE_SHA256
tar -xzf migration_package_20260714.tar.gz
```

The restored package contains the UniMol core code, reproducible datasets, selected checkpoints, runtime environment notes, and the project handoff document.
