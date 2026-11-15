# Input data

Place these files here, without renaming them:

- `primary-screen-cell-line-info.csv`
- `primary-screen-replicate-collapsed-logfold-change.csv`
- `primary-screen-replicate-collapsed-treatment-info.csv`
- `sample_info.csv`

The first three are primary-screen downloads from https://depmap.org/repurposing/ . The final file is DepMap cell-line metadata, available through https://depmap.org/portal/download/all/ ; the release of the initial local copy is unverified. Record the release and download URL when resolving provenance. Do not silently replace it with another release.

Local copies were imported from existing downloads; the original download files were preserved. `docs/data_manifest.json` records SHA-256 hashes and sizes of the specific inputs used. Raw CSVs are intentionally ignored by Git.
