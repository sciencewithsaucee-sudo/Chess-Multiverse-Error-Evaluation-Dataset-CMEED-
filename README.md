# Chess Multiverse Error & Evaluation Dataset (CMEED v1.0)

## 🚀 Live Interactive Explorer

Explore the dataset visually through the Chess Multiverse platform:

👉 **https://www.chessmultiverse.org**

The CMEED dataset powers error analytics, player error profiling, opening mistake exploration, and large-scale chess research tools developed by Chess Multiverse.

---

## 📊 Dataset Overview

The **Chess Multiverse Error & Evaluation Dataset (CMEED)** is a large-scale open-source chess research dataset containing engine-annotated player errors extracted from professional and competitive chess broadcasts.

CMEED records every detected:

* Inaccuracy
* Mistake
* Blunder

along with the complete board position before and after the move, engine evaluation changes, clock information, player ratings, opening metadata, and game identifiers.

Version 1.0 contains data extracted from official Lichess Broadcast events spanning **January 2026 through May 2026**.

---

## 📈 Dataset Statistics

| Metric                | Value                   |
| --------------------- | ----------------------- |
| Dataset Version       | CMEED v1.0              |
| Coverage Period       | January 2026 – May 2026 |
| Total Error Records   | 994,269                 |
| Total Games Processed | 139,000+                |
| Inaccuracies          | 572,000+                |
| Mistakes              | 196,000+                |
| Blunders              | 226,000+                |
| Storage Size          | ~1.33 GB                |
| Format                | JSON                    |
| License               | CC BY-SA 4.0            |

---

## 📁 Repository Structure

```text
data/
├── cmeed_2026-01.json
├── cmeed_2026-02.json
├── cmeed_2026-03.json
├── cmeed_2026-04.json
└── cmeed_2026-05.json
```

Each file contains all extracted error records for the corresponding month.

---

## 🗄️ Data Schema (Data Dictionary)

Each JSON object represents a single detected player error.

| Key            | Type    | Description                     |
| -------------- | ------- | ------------------------------- |
| error_id       | String  | Unique error identifier         |
| game_id        | String  | Unique game identifier          |
| source_file    | String  | Original PGN source file        |
| event          | String  | Tournament or event name        |
| broadcast_name | String  | Broadcast title                 |
| game_url       | String  | Original game URL               |
| eco            | String  | ECO opening code                |
| opening        | String  | Opening name                    |
| date           | String  | Game date                       |
| year           | Integer | Year                            |
| round          | String  | Tournament round                |
| board          | String  | Board number                    |
| white          | String  | White player                    |
| black          | String  | Black player                    |
| player         | String  | Player committing the error     |
| white_elo      | Integer | White rating                    |
| black_elo      | Integer | Black rating                    |
| player_elo     | Integer | Error-maker rating              |
| white_title    | String  | White title                     |
| black_title    | String  | Black title                     |
| player_fide_id | String  | FIDE ID                         |
| result         | String  | Game result                     |
| time_control   | String  | Time control                    |
| move_number    | Integer | Move number                     |
| error_ply      | Integer | Ply number                      |
| side           | String  | White or Black                  |
| opening_phase  | String  | Opening, Middlegame, Endgame    |
| error_type     | String  | Inaccuracy, Mistake, or Blunder |
| played_move    | String  | Move played                     |
| best_move      | String  | Engine best move                |
| eval_before    | Float   | Evaluation before move          |
| eval_after     | Float   | Evaluation after move           |
| eval_change    | Float   | Absolute evaluation swing       |
| clock_seconds  | Integer | Remaining clock time            |
| fen_before     | String  | Position before move            |
| fen_after      | String  | Position after move             |

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

Custom CMEED extraction software parses PGN annotations and identifies:

* Inaccuracies
* Mistakes
* Blunders

using engine annotations embedded within the broadcast PGNs.

### 3. Position Reconstruction

Every move is replayed using python-chess to reconstruct:

* FEN before the move
* FEN after the move

allowing precise position-level analysis.

### 4. Evaluation Tracking

For every error:

```text
eval_before
eval_after
eval_change
```

are reconstructed from engine evaluations present in the PGN comments.

### 5. Metadata Enrichment

Tournament, player, rating, title, opening, time control, and game identifiers are attached to every record.

---

## 💻 Example Usage

### Python

```python
import pandas as pd
import json

with open("cmeed_2026-05.json", "r", encoding="utf-8") as f:
    data = json.load(f)

df = pd.DataFrame(data)

carlsen = df[df["player"] == "Carlsen, Magnus"]

print(carlsen["error_type"].value_counts())
```

### Find Largest Blunders

```python
blunders = df[df["error_type"] == "Blunder"]

largest = blunders.sort_values(
    by="eval_change",
    ascending=False
)

print(largest.head())
```

---

## 🔬 Research Applications

CMEED enables research in:

* Chess Performance Analytics
* Human Error Modeling
* Opening Preparation
* Decision Making Under Time Pressure
* Elo-Based Error Prediction
* Endgame Error Analysis
* Tournament-Level Statistical Research
* Machine Learning for Human Chess Behavior

---

## 🤝 Contributing

Contributions are welcome.

Potential areas include:

* Additional years
* More tournaments
* Additional engine metrics
* Position classification
* Research notebooks
* Data validation tools

Issues and pull requests are encouraged.

---

## 📝 Citation

If you use CMEED in academic work, please cite:

> Varshney, S. (2026). *Chess Multiverse Error & Evaluation Dataset (CMEED v1.0)*. Chess Multiverse Lab. DOI: Coming Soon.

---

## 👨‍🔬 Lead Researcher & Principal Developer

**Sparsh Varshney**

Founder, Chess Multiverse

* Chess Research
* Open Data Science
* Chess Analytics
* AI & Data Engineering

Projects:

* Chess Multiverse
* Amidha Ayurveda

GitHub:
https://github.com/sciencewithsaucee-sudo

ORCID:
https://orcid.org/0009-0004-7835-0673

---

## ⚖️ License

This dataset is released under the **Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)** License.

You are free to:

* Share
* Adapt
* Build upon

for any purpose, including commercial use, provided proper attribution is given and derivative works are distributed under the same license.
