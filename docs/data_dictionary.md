# Data dictionary

## Responses

Rows identify cell lines; columns identify treatment conditions. Values are processed log-fold-change viability measurements relative to controls. Negative values indicate lower relative signal; zero is approximately control-like. Missing values are unobserved responses, not zero effect. Replicates have already been combined. Verify normalization details against upstream documentation before converting values to percentages.

## Screen cell metadata

`row_name` joins to the response row. `depmap_id` is the confirmed identifier used to join `sample_info.DepMap_ID`. `passed_str_profiling` describes the DNA fingerprint identity check; `str_profiling_notes` records issues. Do not repair failed identities using `originally_assigned_depmap_id`.

## Treatments

`column_name` is the complete response-column key. `broad_id` identifies the compound record; `name` is a readable label, not a unique join key. `dose` records concentration, and `screen_id` the screen. `moa` describes annotated mechanism of action; `target` lists annotated biological targets. `smiles` encodes chemical structure. `disease.area`, `indication`, and `phase` describe existing uses/development annotations, not findings of this project. Confirm units against the source documentation before labeling dose plots.

## DepMap samples

`DepMap_ID` is the unique join key. `cell_line_name`, `lineage`, `primary_disease`, and `Subtype` describe the cell model. This is a catalog larger than the PRISM screen. It contains no expression matrix. CRISPR-related fields such as `Achilles_n_replicates` are not PRISM replicate counts.
