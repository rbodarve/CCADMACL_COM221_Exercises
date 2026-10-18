This repository is for Advance Machine Learning Subject (CCADMACL) Exercises

## Review notes (2026-10-18)

- Setup: dota2.ipynb reads OPENDOTA_API_KEY from a gitignored .env file (one line: OPENDOTA_API_KEY=your_key).
- Security: a hardcoded API key was removed from the whole git history on 2026-10-18 (history rewritten; commit hashes changed).
- Data: tv_show_posters/ (6384 posters, 1.5 GB) was removed from git history on 2026-10-18 and is gitignored; imdbscrape.ipynb can re-download it. old_imdb_episodes.csv and tv_posters/ are not used by any notebook.
- Drafts: finalAnalysis, finalAnalysis2, finalAnalysis3 and imdbtempanalysis are versions of one poster PCA/clustering analysis; the repo does not record which version was submitted.
- Known bugs (as submitted, not fixed; cell = 0-based code-cell index):
  - imdbimage cell 0: the URL loses its domain, so every request fails silently and top_tv_shows_complete.csv has only a header; show 250 is skipped.
  - Iris PCA cell 10: `iris.feature_names` raises NameError (the dataset variable is `sf`).
  - 3 cell 4: `pd.concat([features, target])` stacks rows instead of columns; later cells use the resulting NaN-filled data.
  - 3 cell 8: `preprocessing.normalize` scales rows, not columns, so the clusters, elbow and silhouette are not meaningful.
  - Midterm cell 2: selects `seriesID`, which is not an IMDb episode column, and overwrites output_file.csv.
  - Midterm cell 22: `find_best_dbscan_params` can return None, which crashes the next line; the face target is 4 clusters here but 3 in cells 11 and 17.
  - finalAnalysis cell 4, rgbw_with_label cell 0: `r+g+b` on uint8 overflows, so the "white" feature is wrong.
  - imdbscrape cell 5: `range(7749, len(df)+1)` raises IndexError on the last step and skips earlier rows.
  - Exercise1 cell 10: VarianceThreshold runs on unscaled data that includes the target, so the filter feature set is arbitrary.
  - Exercise1 cells 19, 23: RFE and SelectFromModel are fit before the train/test split (data leakage).
  - Exercise1 cells 6, 15, 22, 26: `sm.OLS` is fit on the test set without an intercept, so the reported R² is inflated.
  - 2 cell 7: `dropna()` runs on train only, so train and test are prepared differently.
  - 2 cell 15: RMSLE raises an error if any prediction is negative; predictions are not clipped.
  - imdbtempanalysis cell 4: the LBP histogram has 9 bins for 10 labels, so label 9 is dropped.
  - finalAnalysis3 cell 4: the image is RGB but the channels are named blue/green/red, so the blue and red features are swapped.
- Missing inputs: train.csv/test.csv/sample_submission.csv (2), creditcard.csv (4), title.episode.tsv (Midterm), F:/dataset (rgbw_with_label), imdb_show_images/ (finalAnalysis2). The Midterm datasets on github.com/robitussin/CCADMACL_EXAM return HTTP 404.
- Run check 2026-10-18 (ml env, CPU): 3 and Exercise1 run top to bottom. Iris PCA stops at code cell 10 (NameError 'iris'). Midterm stops at cell 1 (missing TSV), then at cell 3 (404). The other 12 notebooks were not run (live scraping/API or missing data).
