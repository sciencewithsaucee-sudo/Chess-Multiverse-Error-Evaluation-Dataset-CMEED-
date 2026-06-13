# Chess Multiverse Error & Evaluation Dataset (CMEED v1.0)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20625716.svg)](https://doi.org/10.5281/zenodo.20625716)
[![Dataset](https://img.shields.io/badge/Dataset-CMEED_v1.0-blue)]()
[![Format](https://img.shields.io/badge/Format-JSON-green)]()
[![License](https://img.shields.io/badge/License-CC--BY--SA--4.0-orange)]()
[![Records](https://img.shields.io/badge/Records-994,269-red)]()
## 🚀 Live Interactive Explorer

Explore CMEED through the Chess Multiverse Error Explorer:

https://www.chessmultiverse.org/p/chess-multiverse-error-explorer.html

The explorer enables interactive investigation of:

* Error distributions
* Opening risk profiles
* Player error fingerprints
* Tournament pressure effects
* Position-level error records
* Large-scale chess analytics

The CMEED dataset powers research tools developed through Chess Multiverse.

---

# 📊 Dataset Overview

The **Chess Multiverse Error & Evaluation Dataset (CMEED)** is a large-scale open-source chess research dataset containing structured human decision-making errors extracted from official chess broadcasts.

Unlike traditional chess databases that primarily focus on games, openings, or engine evaluations, CMEED focuses specifically on **player mistakes and decision quality**.

Each record captures a single:

* Inaccuracy
* Mistake
* Blunder

along with:

* Board position before the move
* Board position after the move
* Engine evaluation changes
* Remaining clock time
* Player ratings
* Player titles
* Opening metadata
* Tournament metadata
* Full FEN reconstruction

Version 1.0 contains data extracted from official broadcast events spanning **January 2026 through May 2026**.

---

# 📚 Source Data & Provenance

CMEED is derived from the official Lichess Broadcast Database.

Source broadcasts are distributed under the **Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0)** license.

The source PGNs contain:

* Engine evaluations
* Clock information
* Opening metadata
* Tournament metadata
* Player metadata

CMEED transforms these raw broadcast PGNs into a structured research dataset focused on human error behavior.

Transformation pipeline:

```text
Broadcast PGN
    ↓
Evaluation Parsing
    ↓
Error Detection
    ↓
Position Reconstruction
    ↓
Metadata Enrichment
    ↓
CMEED Dataset
```

---

# 📈 Dataset Statistics

| Metric              | Value                   |
| ------------------- | ----------------------- |
| Dataset Version     | CMEED v1.0              |
| Coverage Period     | January 2026 – May 2026 |
| Games               | 106,911                 |
| Total Error Records | 994,269                 |
| Unique Players      | 32,203                  |
| Opening Families    | 489                     |
| Inaccuracies        | 566,830                 |
| Mistakes            | 195,775                 |
| Blunders            | 231,664                 |
| Storage Size        | ~1.33 GB                |
| Format              | JSON                    |
| License             | CC BY-SA 4.0            |

---

# 📦 Monthly Dataset Breakdown

| Month         | Error Records |
| ------------- | ------------: |
| January 2026  |       186,544 |
| February 2026 |       130,945 |
| March 2026    |       205,046 |
| April 2026    |       201,910 |
| May 2026      |       269,824 |
| **Total**     |   **994,269** |

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
├── cmeed_v1.parquet
├── README.md
├── CITATION.cff
├── LICENSE
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
└── .gitattributes
```

### Dataset Formats

CMEED is distributed in two formats:

| Format | Description |
|----------|----------|
| JSON | Monthly source datasets |
| Parquet | Consolidated research dataset |

The Parquet release contains all 994,269 error records in a compressed columnar format optimized for analytics, machine learning, and large-scale research workflows.

Researchers are encouraged to use the Parquet release for maximum performance.

---

# 🗄️ Data Schema (Data Dictionary)

Each JSON object represents a single detected player error.

| Field          | Type    | Description                  |
| -------------- | ------- | ---------------------------- |
| error_id       | String  | Unique error identifier      |
| game_id        | String  | Unique game identifier       |
| source_file    | String  | Source dataset file          |
| event          | String  | Tournament name              |
| broadcast_name | String  | Broadcast title              |
| game_url       | String  | Original game URL            |
| eco            | String  | ECO code                     |
| opening        | String  | Opening name                 |
| date           | String  | Game date                    |
| year           | Integer | Year                         |
| round          | String  | Tournament round             |
| board          | String  | Board number                 |
| white          | String  | White player                 |
| black          | String  | Black player                 |
| player         | String  | Player committing the error  |
| white_elo      | Integer | White rating                 |
| black_elo      | Integer | Black rating                 |
| player_elo     | Integer | Player rating                |
| white_title    | String  | White title                  |
| black_title    | String  | Black title                  |
| player_fide_id | String  | FIDE identifier              |
| result         | String  | Game result                  |
| time_control   | String  | Time control                 |
| move_number    | Integer | Move number                  |
| error_ply      | Integer | Ply number                   |
| side           | String  | White or Black               |
| opening_phase  | String  | Opening, Middlegame, Endgame |
| error_type     | String  | Inaccuracy, Mistake, Blunder |
| played_move    | String  | Move played                  |
| best_move      | String  | Engine recommendation        |
| eval_before    | Float   | Evaluation before move       |
| eval_after     | Float   | Evaluation after move        |
| eval_change    | Float   | Evaluation swing             |
| clock_seconds  | Integer | Remaining clock time         |
| fen_before     | String  | Position before move         |
| fen_after      | String  | Position after move          |

---

# 🧪 Methodology

## 1. Data Collection

Games were collected from official broadcast PGN archives.

## 2. Error Extraction

Custom CMEED extraction software identifies:

* Inaccuracies
* Mistakes
* Blunders

from engine annotations embedded within broadcast PGNs.

## 3. Position Reconstruction

Every game is replayed using **python-chess** to reconstruct:

* FEN before move
* FEN after move

for each detected error.

## 4. Evaluation Tracking

For every error record:

* eval_before
* eval_after
* eval_change

are extracted and reconstructed from engine evaluations embedded in PGN annotations.

## 5. Metadata Enrichment

Each record is enriched with:

* Tournament metadata
* Player metadata
* Rating information
* Opening information
* Clock information
* Game identifiers

---

# 🔁 Reproducibility

CMEED was generated using the Chess Multiverse Error Extraction Pipeline.

Core technologies:

* Python
* python-chess
* PGN parsing
* JSON serialization

Pipeline:

```text
PGN Import
    ↓
Evaluation Parsing
    ↓
Error Detection
    ↓
FEN Reconstruction
    ↓
Metadata Enrichment
    ↓
JSON Export
```

---

# 💻 Example Usage

## Load Dataset

```python
import json
import pandas as pd

with open("data/cmeed_2026-05.json", "r", encoding="utf-8") as f:
    data = json.load(f)

df = pd.DataFrame(data)

print(df.head())
```

## Player Error Analysis

```python
carlsen = df[df["player"] == "Carlsen, Magnus"]

print(carlsen["error_type"].value_counts())
```

## Largest Blunders

```python
blunders = df[df["error_type"] == "Blunder"]

largest = blunders.sort_values(
    by="eval_change",
    ascending=False
)

print(largest.head())
```

## Opening Error Analysis

```python
opening_errors = (
    df.groupby("opening")
      .size()
      .sort_values(ascending=False)
)

print(opening_errors.head(20))
```

---

# 🔬 Research Applications

CMEED enables research in:

* Human Error Modeling
* Chess Performance Analytics
* Opening Risk Assessment
* Time Pressure Studies
* Decision-Making Research
* Elo-Based Error Prediction
* Endgame Error Analysis
* Tournament-Level Statistical Research
* Cognitive Science
* Sports Analytics
* Artificial Intelligence
* Machine Learning
* Reinforcement Learning
* Explainable AI
* Human-Computer Interaction
* Chess Education

---

# ⚠️ Limitations

* Coverage is limited to official broadcast events available through the source archive.
* Error detection depends on engine evaluations embedded within source PGNs.
* CMEED focuses on inaccuracies, mistakes, and blunders rather than every move played.
* Version 1.0 covers January 2026 through May 2026 only.
* Additional tournaments and historical years may be added in future releases.

---

# 🤝 Contributing

Contributions are welcome.

Please read:

* CONTRIBUTING.md
* CODE_OF_CONDUCT.md

before submitting issues or pull requests.

Potential areas include:

* Additional years
* Additional tournaments
* Validation tooling
* Data quality improvements
* Research notebooks
* Visualization tools
* Position classification systems

---

# 📝 Citation

If you use CMEED in research, publications, software, educational projects, or derivative datasets, please cite the dataset.

```text
Varshney, Sparsh. (2026). Chess Multiverse Error & Evaluation Dataset (CMEED v1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.20625716
```

## DOI

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20625716.svg)](https://doi.org/10.5281/zenodo.20625716)

DOI: https://doi.org/10.5281/zenodo.20625716

---

# 👨‍🔬 Lead Researcher & Principal Developer

**Sparsh Varshney**

Founder, Chess Multiverse

Research Interests:

* Chess Analytics
* Human Error Modeling
* Open Data Science
* Artificial Intelligence
* Medical Research
* Open Science

## Projects

### Chess Multiverse

https://www.chessmultiverse.org

### Amidha Ayurveda

https://www.amidhaayurveda.com

## Profiles

GitHub:

https://github.com/sciencewithsaucee-sudo

ORCID:

https://orcid.org/0009-0004-7835-0673

---

# ⚖️ License

This dataset is released under the Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0).

You are free to:

* Share
* Adapt
* Build upon the dataset

for any purpose, including commercial use, provided appropriate attribution is given and derivative works are distributed under the same license.

See the LICENSE file for full details.
