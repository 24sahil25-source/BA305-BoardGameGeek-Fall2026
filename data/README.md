# Data

The raw BoardGameGeek files for the BA305 term project, team A8, kept exactly as downloaded. Derived datasets are produced by notebooks and saved under new names.

## Source

- Pool dataset 5, "BoardGameGeek game catalogue", allocated to team A8 on 2026-09-11.
- Downloaded unmodified on 2026-10-13 from the TidyTuesday repository, week 2022-01-25: <https://github.com/rfordatascience/tidytuesday/tree/main/data/2022/2022-01-25>
- TidyTuesday took the data from Kaggle ("BoardGameGeek reviews", snapshot dated 2022-01-08), which collected it from <https://www.boardgamegeek.com/>.
- The two files join on `id`.

## Files

| File | Rows | Columns | Size |
| --- | --- | --- | --- |
| `ratings.csv` | 21,831 | 10 | 5.0 MB |
| `details.csv` | 21,631 | 23 | 34.3 MB (the `description` column is most of it) |

## Column dictionary

From the TidyTuesday readme, descriptions as given there.

### `ratings.csv`

| Column | Type | Description |
| --- | --- | --- |
| `num` | number | Game number |
| `id` | number | Game ID |
| `name` | text | Game name |
| `year` | number | Game year |
| `rank` | number | Game rank |
| `average` | number | Average rating |
| `bayes_average` | number | Bayes average rating |
| `users_rated` | number | Users rated |
| `url` | text | Game url |
| `thumbnail` | text | Game thumbnail |

### `details.csv`

| Column | Type | Description |
| --- | --- | --- |
| `num` | number | Game number |
| `id` | number | Game ID |
| `primary` | text | Primary name |
| `description` | text | Description of game |
| `yearpublished` | number | Year published |
| `minplayers` | number | Min n of players |
| `maxplayers` | number | Max n of players |
| `playingtime` | number | Playing time in minutes |
| `minplaytime` | number | Min play time |
| `maxplaytime` | number | Max play time |
| `minage` | number | Minimum age |
| `boardgamecategory` | text, list | Category |
| `boardgamemechanic` | text, list | Mechanic |
| `boardgamefamily` | text, list | Board game family |
| `boardgameexpansion` | text, list | Expansion |
| `boardgameimplementation` | text, list | Implementation |
| `boardgamedesigner` | text, list | Designer |
| `boardgameartist` | text, list | Artist |
| `boardgamepublisher` | text, list | Publisher |
| `owned` | number | Num owned |
| `trading` | number | Num trading |
| `wanting` | number | Num wanting |
| `wishing` | number | Num wishing |

## Facts worth knowing before you use the files (checked 2026-10-13)

- 200 ids in `ratings.csv` have no row in `details.csv`. An inner join on `id` gives 21,631 games. `year` and `yearpublished` agree in 99.95% of rows.
- Every game has at least 30 user ratings (`users_rated` minimum is 30).
- Zero is used to mean "unknown" in `minage` (1,301 rows), `maxplayers` (164), `minplayers` (44), `minplaytime` (642), `playingtime` and `maxplaytime` (774), and `yearpublished` (195 rows at 0 or below; BoardGameGeek uses negative years for games from before year 1).
- `playingtime` equals `maxplaytime` in every row.
- Extreme values exist: `maxplayers` up to 999, `playingtime` up to 60,000 minutes.
- The list columns are stored as Python-list text, for example `['Dice Rolling', 'Hand Management']`.
- There is no complexity or "weight" column in this cut of the data.

## Loading

```python
import pandas as pd

BASE = "https://raw.githubusercontent.com/24sahil25-source/BA305-BoardGameGeek-Fall2026/main/data/"
ratings = pd.read_csv(BASE + "ratings.csv")
details = pd.read_csv(BASE + "details.csv")
```
