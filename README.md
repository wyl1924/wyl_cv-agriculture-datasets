# wyl_cv agriculture V2 research datasets

Dataset-only release `agriculture-v2-research-datasets-2026-09-07`. It contains the exact five frozen
train/val image sets used by the selected V2 research candidates, after a
privacy transform that is lossless for each retained primary image. It contains
no application code, model weights,
raw archives, OOD, reserve, quarantine, review, cache, superseded, or unfinished
data.

| Dataset | Task | Images | Classes |
| --- | --- | ---: | ---: |
| `corn-leaf-disease-v2` | classification | 6,519 | 9 |
| `corn-field-pest-v2` | classification | 2,898 | 5 |
| `maize-herbivory-damage-v2` | classification | 14,577 | 4 |
| `cotton-bollworm-det-v2` | detection | 3,173 | 1 |
| `karaagro-faw-larva-det-v2-1` | detection | 2,711 | 1 |

Total: **29,878 images**. These are separate modules,
not one flat classifier. The frozen target is 17 biotic classes plus one healthy
control; model heads contain repeated semantics and one auxiliary class. The
frozen scope still has no honest training set for maize rough dwarf or
*Ostrinia furnacalis*; no substitute label is used.

## Safety status

All five datasets and their models are research-only. They have no independent
China-field blind test and do not support automatic diagnosis. Classification
models have no calibrated unknown/OOD rejection threshold. Detector boxes must
be reviewed by a person. See each `dataset.json` and `ATTRIBUTION.md`.

## Layout

- `datasets/*/manifest.csv`: pseudonymous paths, privacy-safe group IDs, and
  published-file integrity hashes. For detector datasets, `label` is the image
  stratum (`positive`/`negative`), while `classes` in `dataset.json` is the
  object class.
- `datasets/*/dataset.json`: task, classes, counts, sources, and limitations.
- `datasets/*/data.yaml`: relative-path YOLO configuration for detectors.
- `release-assets.json` and `SHA256SUMS`: release asset inventory.
- `PRIVACY.md`: lossless metadata-removal contract and verification.
- `RESTORE.md`: download, verify, and extract steps.

The repository has no blanket license over third-party images. Each image keeps
its upstream source license, identified by `source_id`; attribution and license
links are in `ATTRIBUTION.md`. PlantVillage files remain CC BY-SA 3.0.
