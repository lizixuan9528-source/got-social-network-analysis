# 🐺 Game of Thrones Social Network Dataset (Seasons 1-3)

---

## 📂 Files Included

1.  **`got_nodes_clean.csv`**: Comprehensive node attribute list for all unique, named characters (N=203).
2.  **`got_edges_clean.csv`**: The undirected edge list representing character interactions (E=1041).
3.  **`got_s1_s3_nodes.csv`**: Initial node list of season 1-3 derived from [mathbeveridge/gameofthrones](https://github.com/mathbeveridge/gameofthrones).
4.  **`got_s1_s3_edges.csv`**: Initial edge list of season 1-3.

---

## 📖 Data Dictionary

### 1. Node Attributes (`got_nodes_clean.csv`)
This file contains demographic, narrative, and network features for characters, refined through API fetching and expert manual imputation.

| Variable | Type | Description |
| :--- | :--- | :--- |
| **`Original_Name`** | `String` | The unique character ID from the raw interaction data (e.g., "JON", "LITTLEFINGER"). **Primary key for merging with the Edge List.** |
| **`label`** | `String` | Clean, readable full name (e.g., "Jon Snow", "Petyr Baelish"). Formatted for automatic recognition by `igraph` for plotting. |
| **`Degree`** | `Integer` | Unweighted degree: The number of unique individuals this character is directly connected to. |
| **`Strength`** | `Integer` | Weighted degree: The total frequency of all interactions across the first three seasons. |
| **`Gender`** | `String` | Character's gender: `Male`, `Female`, or `Unknown`. |
| **`Is_Noble`** | `Binary` | Nobility indicator: `1` = Royalty or High Nobility (Lords/Ladies), `0` = Others (Knights, Smallfolk, etc.). |
| **`House`** | `String` | Political Tier categorization: `Great_Houses` (The 9 Major Houses), `Minor_Houses` (Vassal families), or `None`. |
| **`Culture`** | `String` | Geographical/Cultural grouping: `North_and_Wildlings`, `Westeros_South`, `Essos`, or `None`. |
| **`Titles`** | `String` | Social/Professional class: `Royalty`, `Official`, `Military_Knight`, `Nobility`, `Religion_Academic`, or `None`. |
| **`Active`** | `Integer` | The number of POV (Point of View) chapters the character has in the source novels. Acts as a proxy for narrative importance. |
| **`Survival`** | `Binary` | Survival status by the end of Season 3: `1` = Survived, `0` = Deceased. |

### 2. Edge List (`got_edges_clean.csv`)
Represents the **undirected** social ties between characters.

* **`Source`** / **`Target`**: The `Original_Name` of the two interacting characters.
* **`Weight`**: The intensity of the relationship (based on scene co-occurrence or dialogue frequency).

---

## 🛡️ Data Cleaning Methodology

This dataset underwent the following rigorous preprocessing steps:

* **Nameless Filtering**: Utilized advanced Regex to strip out generic professional titles (e.g., *Assassin, Prostitute, Messenger*). This prevents "ghost nodes" from creating false brokerage effects in the network topology.
* **TV-to-Book Alignment**: Addressed show-exclusive characters (e.g., *Ros*) and name discrepancies (e.g., *Yara Greyjoy* vs. *Asha Greyjoy*) to ensure high-quality API hits.
* **Manual Imputation**: For 14 critical nodes not found in standard APIs (e.g., *Eddison Tollett, Myranda, Olyvar, Radzai Mo Eraz*), attributes were manually populated using domain expertise to ensure 100% data completeness for statistical modeling.
* **Categorical Consolidation**: Merged sparse House categories into a three-tier hierarchy (`Great`, `Minor`, `None`) to increase statistical power for Logistic Regression and avoid over-fitting due to sparse data.

---

## 🛠️ Data Sources & Acknowledgements
* **Edge Data:** Derived and expanded from [mathbeveridge/gameofthrones](https://github.com/mathbeveridge/gameofthrones).
* **Node Attributes:** Aggregated via [An API of Ice and Fire](https://anapioficeandfire.com/) and cross-referenced with the HBO *Game of Thrones* series.
