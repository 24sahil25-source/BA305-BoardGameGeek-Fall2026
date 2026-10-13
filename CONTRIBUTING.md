# Contributing

How work is organized in this repository and how changes get in.

## Notebooks

- One notebook per person per piece of work, in `notebooks/`, named `NN_topic_handle.ipynb`, for example `02_descriptive_charts_rowanj.ipynb`. The number orders the pipeline; the handle identifies the owner.
- The first cell of every notebook names its author and purpose:
  ```python
  # --- Firstname Lastname: what this notebook does ---
  ```
- Cells written with AI assistance carry a label on their first line. All such use is disclosed in the final report's appendix.
  ```python
  # [AI-assisted] <tool> (<model>), <date>. <what it generated>; reviewed and edited by <name>.
  ```
- Notebooks load data from this repository by URL (cell below), so they run unchanged in Colab and locally.
- A notebook is done when it runs top to bottom from a fresh kernel.

## Two ways to contribute

### From Colab

1. File > Open notebook > GitHub tab > `24sahil25-source/BA305-BoardGameGeek-Fall2026`. Open the notebook from there rather than from a Drive copy, so it starts from the latest saved version. Colab asks for GitHub authorization the first time.
2. Work, then File > Save a copy in GitHub: this repository, branch `main`, path `notebooks/NN_topic_handle.ipynb`, a short commit message. The commit appears under your account.

Saving writes the file at that path directly; it does not merge. That is why each notebook has a single owner.

### With git

1. `git clone https://github.com/24sahil25-source/BA305-BoardGameGeek-Fall2026.git`
2. `git switch main && git pull && git switch -c handle/topic`
3. Edit, then `git add`, `git commit -m "short description"`, `git push -u origin handle/topic`
4. Open a pull request on GitHub. Anyone on the team can review it in the browser. Merge with "Create a merge commit", which keeps each commit's author.

## Review checklist

- Runs top to bottom from a fresh kernel.
- Author line in cell 1; AI labels where applicable.
- Charts have a title, labelled axes with units, a legend or direct labels, and a caption stating the takeaway.
- Predictive notebooks use no post-outcome columns as features (`rank`, `bayes_average`, `users_rated`, `owned`, `trading`, `wanting`, `wishing`, `boardgameexpansion`, `boardgameimplementation`), and fit scalers, encoders, and imputers on training rows only.

## Data and figures

- `data/` holds the raw files exactly as downloaded. Derived datasets are produced by notebooks and committed together with them.
- Figures for the report are saved to `figures/` with `plt.savefig("figures/name.png", dpi=300, bbox_inches="tight")`.

## Data-loading cell

```python
import pandas as pd

BASE = "https://raw.githubusercontent.com/24sahil25-source/BA305-BoardGameGeek-Fall2026/main/data/"
ratings = pd.read_csv(BASE + "ratings.csv")
details = pd.read_csv(BASE + "details.csv")
```

Analysis notebooks switch to `data/bgg_clean.csv` once the cleaning notebook has produced it.

---

Drafted with Claude Code assistance.
