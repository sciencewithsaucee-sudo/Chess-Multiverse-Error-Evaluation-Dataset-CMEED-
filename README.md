# Chess Multiverse Error & Evaluation Dataset (CMEED v1.0)

[![Dataset](https://img.shields.io/badge/Dataset-CMEED_v1.0-blue)]()
[![Format](https://img.shields.io/badge/Format-JSON-green)]()
[![License](https://img.shields.io/badge/License-CC--BY--SA--4.0-orange)]()
[![Records](https://img.shields.io/badge/Records-994,269-red)]()

## 🚀 Live Interactive Explorer

Explore the dataset visually through the Chess Multiverse platform:

👉 **https://www.chessmultiverse.org**

The CMEED dataset powers error analytics, player error profiling, opening mistake exploration, and large-scale chess research tools developed by Chess Multiverse.

---

## 📊 Dataset Overview

The **Chess Multiverse Error & Evaluation Dataset (CMEED)** is a large-scale open-source chess research dataset containing engine-annotated player errors extracted from official chess broadcasts.

Unlike traditional chess databases that focus on games, openings, or engine evaluations, CMEED focuses specifically on **human decision-making errors**.

Each record captures a single:

- Inaccuracy
- Mistake
- Blunder

along with:

- Complete board position before the move
- Complete board position after the move
- Engine evaluation changes
- Remaining clock time
- Player ratings
- Player titles
- Opening metadata
- Tournament metadata
- Full position reconstruction via FEN

Version 1.0 contains data extracted from official Lichess Broadcast events spanning **January 2026 through May 2026**.

---

## 📈 Dataset Statistics

| Metric | Value |
|----------|----------|
| Dataset Version | CMEED v1.0 |
| Coverage Period | January 2026 – May 2026 |
| Games Processed | 140,662 |
| Broken Games | 0 |
| Total Error Records | 994,269 |
| Inaccuracies | 566,830 |
| Mistakes | 195,775 |
| Blunders | 231,664 |
| Average Errors per Game | 7.07 |
| Storage Size | ~1.33 GB |
| Format | JSON |
| License | CC BY-SA 4.0 |

---

## 📦 Monthly Dataset Breakdown

| Month | Games | Error Records |
|---------|---------:|---------:|
| January 2026 | 25,362 | 186,544 |
| February 2026 | 19,617 | 130,945 |
| March 2026 | 27,401 | 205,046 |
| April 2026 | 31,435 | 201,910 |
| May 2026 | 36,847 | 269,824 |
| **Total** | **140,662** | **994,269** |

---

## 📁 Repository Structure

```text
Chess-Multiverse-Error-Evaluation-Dataset-CMEED/

├── data/
│   ├── cmeed_2026-01.json
│   ├── cmeed_2026-02.json
│   ├── cmeed_2026-03.json
│   ├── cmeed_2026-04.json
│   └── cmeed_2026-05.json
│
├── README.md
├── CITATION.cff
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
└── .gitattributes
```

Each monthly file contains all extracted errors from official chess broadcast games for that month.

---

## 🗄️ Data Schema (Data Dictionary)

Each JSON object represents a single detected player error.

| Field | Type | Description |
|---------|---------|---------|
| error_id | String | Unique error identifier |
| game_id | String | Unique game identifier |
| source_file | String | Original PGN source file |
| event | String | Tournament or event name |
| broadcast_name | String | Broadcast title |
| game_url | String | Original game URL |
| eco | String | ECO opening code |
| opening | String | Opening name |
| date | String | Game date |
| year | Integer | Year |
| round | String | Tournament round |
| board | String | Board number |
| white | String | White player |
| black | String | Black player |
| player | String | Player committing the error |
| white_elo | Integer | White rating |
| black_elo | Integer | Black rating |
| player_elo | Integer | Rating of player committing the error |
| white_title | String | White title |
| black_title | String | Black title |
| player_fide_id | String | FIDE ID |
| result | String | Game result |
| time_control | String | Time control |
| move_number | Integer | Move number |
| error_ply | Integer | Ply number |
| side | String | White or Black |
| opening_phase | String | Opening, Middlegame, Endgame |
| error_type | String | Inaccuracy, Mistake, or Blunder |
| played_move | String | Move played |
| best_move | String | Engine best move |
| eval_before | Float | Evaluation before move |
| eval_after | Float | Evaluation after move |
| eval_change | Float | Absolute evaluation swing |
| clock_seconds | Integer | Remaining clock time |
| fen_before | String | Position before move |
| fen_after | String | Position after move |

---

## 📄 Sample Record

```json
{
  "error_id": "CMEED-2026-05-0040569",
  "game_id": "CMEED-GAME-c0d3bec8c9bd",
  "source_file": "cmeed_2026-05.json",
  "event": "TePe Sigeman Chess Tournament 2026",
  "broadcast_name": "TePe Sigeman & Co Chess Tournament 2026",
  "game_url": "https://lichess.org/broadcast/tepe-sigeman--co-chess-tournament-2026/round-6/PXk4j6f7/Nz0OuQO0",
  "eco": "E73",
  "opening": "King's Indian Defense: Semi-Averbakh System",
  "date": "2026-05-06",
  "year": 2026,
  "round": "6.3",
  "board": "",
  "white": "Woodward, Andy",
  "black": "Carlsen, Magnus",
  "player": "Carlsen, Magnus",
  "white_elo": 2635,
  "black_elo": 2840,
  "player_elo": 2840,
  "white_title": "GM",
  "black_title": "GM",
  "player_fide_id": "1503014",
  "result": "0-1",
  "time_control": "90 minutes for 40 moves + 30 minutes for the rest of the game + 30 seconds per move from move one.",
  "move_number": 39,
  "error_ply": 78,
  "side": "black",
  "opening_phase": "Middlegame",
  "error_type": "Inaccuracy",
  "played_move": "Ng3+",
  "best_move": "Qf6",
  "eval_before": -4.03,
  "eval_after": -3.09,
  "eval_change": 0.94,
  "clock_seconds": 103,
  "fen_before": "6k1/5p2/2ppq2p/7n/1PP1PPp1/3BB3/4K1P1/R7 b - - 0 39",
  "fen_after": "6k1/5p2/2ppq2p/8/1PP1PPp1/3BB1n1/4K1P1/R7 w - - 1 40"
}
```

---

## 🧪 Methodology

### 1. Data Collection

Games were collected from official Lichess Broadcast PGN archives covering major international tournaments and events.

### 2. Error Extraction

Custom CMEED extraction software identifies:

- Inaccuracies
- Mistakes
- Blunders

from engine annotations embedded within broadcast PGNs.

### 3. Position Reconstruction

Every game is replayed using **python-chess** to reconstruct:

- FEN before the move
- FEN after the move

for every detected error.

### 4. Evaluation Tracking

For each error:

```text
eval_before
eval_after
eval_change
```

are reconstructed using engine evaluations embedded in PGN comments.

### 5. Metadata Enrichment

Tournament, player, rating, title, opening, result, clock information, and game identifiers are attached to every error record.

---

## 💻 Example Usage

### Load Dataset

```python
import json
import pandas as pd

with open("data/cmeed_2026-05.json", "r", encoding="utf-8") as f:
    data = json.load(f)

df = pd.DataFrame(data)

print(df.head())
```

### Magnus Carlsen Error Analysis

```python
carlsen = df[df["player"] == "Carlsen, Magnus"]

print(carlsen["error_type"].value_counts())
```

### Largest Blunders

```python
blunders = df[df["error_type"] == "Blunder"]

largest = blunders.sort_values(
    by="eval_change",
    ascending=False
)

print(largest.head())
```

### Opening Error Analysis

```python
opening_errors = (
    df.groupby("opening")
      .size()
      .sort_values(ascending=False)
)

print(opening_errors.head(20))
```

---

## 🔬 Research Applications

CMEED enables research in:

- Human Error Modeling
- Chess Performance Analytics
- Opening Risk Assessment
- Time Pressure Studies
- Decision-Making Research
- Elo-Based Error Prediction
- Endgame Error Analysis
- Tournament-Level Statistical Research
- Cognitive Science
- Sports Analytics
- Artificial Intelligence
- Machine Learning
- Reinforcement Learning
- Explainable AI
- Human-Computer Interaction
- Chess Education

---

## 🤝 Contributing

Contributions are welcome.

Please read:

- `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md`

before submitting issues or pull requests.

Potential areas include:

- Additional years
- Additional tournaments
- Validation tooling
- Data quality improvements
- Research notebooks
- Visualization tools
- Position classification systems

---

## 📝 Citation

If you use CMEED in research, publications, software, educational projects, or derivative datasets, please cite the dataset.

### Citation Metadata

See:

```text
CITATION.cff
```

### DOI

Zenodo DOI will be added upon first public release.

---

## 👨‍🔬 Lead Researcher & Principal Developer

**Sparsh Varshney**

Founder, Chess Multiverse

Research Interests:

- Chess Analytics
- Open Data Science
- Human Error Modeling
- Artificial Intelligence
- Medical Research
- Open Science

### Projects

♟️ Chess Multiverse

https://www.chessmultiverse.org

🌿 Amidha Ayurveda

https://www.amidhaayurveda.com

### Profiles

GitHub:
https://github.com/sciencewithsaucee-sudo

ORCID:
https://orcid.org/0009-0004-7835-0673

---

## ⚖️ License

This dataset is released under the Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) License.

You are free to:

- Share
- Adapt
- Build Upon

for any purpose, including commercial use, provided appropriate attribution is given and derivative works are distributed under the same license.

Full license text is available in the LICENSE file.
