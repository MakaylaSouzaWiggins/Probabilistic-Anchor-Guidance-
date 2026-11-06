# Anchor objects provide probabilistic guidance during visual search

**Authors:** Makayla Souza-Wiggins and Joy J. Geng  
**Affiliation:** University of California, Davis  

This repository contains the data, analysis code, and experiment code accompanying the journal article.

---

## Repository Structure

```
ProbAnchors_Materials/
├── Data and Analysis Code/
│   ├── etmsw_final_analyses.Rmd   # All analyses and figures reported in the paper
│   ├── fixations_main.csv          # Main eye-tracking fixation data
│   ├── fixations_ranked.csv        # Fixation data with anchor rank annotations
│   ├── memory_probe_50px.csv       # Memory probe accuracy data (50px hit criterion)
│   ├── anchor_rankings.csv         # Anchor object probability rankings
│   ├── anchor_distribution.csv     # Rank-1 anchor full distribution
│   └── scene_object_counts.csv     # Object counts per scene
├── Experiment Code/
│   ├── etmsw_script_final.py       # Python experiment script (SR Research EyeLink)
│   └── trial_randomization_sheet.csv  # Trial order and condition assignments
└── 
```

---

## Data Dictionary

### fixations_main.csv
Row = one fixation event.

| Column | Description |
|---|---|
| `subject_id` | Participant identifier |
| `trial_No` | Trial number within session |
| `trial_name.y` | Trial screen label (e.g. `Scene_Screen_1`) |
| `fixation_duration` | Duration of fixation in milliseconds |
| `fixation_x` / `fixation_y` | Fixation coordinates on screen |
| `scene_visibility` | Scene visibility condition (`high`, `low`) |
| `target_validity` | Whether anchor predicted target location (`valid`, `invalid`) (in the paper valid is congruent and invalid is incongruent)|
| `target_present` | Whether target was present on the trial (`True`, `False`) |
| `accuracy` | Search accuracy (1 = correct, 0 = incorrect) |
| `rt` | Response time in milliseconds |
| `fixated_object` | Object label fixated on this fixation |
| `target_nanme` | Target object name (note: typo in original data) |
| `valid_anchor` | Name of the rank-1 anchor object for this scene/target |
| `memory_probe_click` | Participant's memory probe response |

### fixations_ranked.csv
Row = one fixation event, with anchor rank and target distance annotations.

Includes all columns from `fixations_main.csv`, plus:

| Column | Description |
|---|---|
| `anchor_fixation` | 1 if fixation landed on the valid (rank-1) anchor |
| `target_fixation` | 1 if fixation landed on the target |
| `dist_to_target_px` | Pixel distance from fixation to target center |
| `within_50px` | 1 if fixation was within 50px of target |

### memory_probe_50px.csv
Row = one memory probe trial (one row per trial, not per fixation).

Includes shared identifier columns, plus:

| Column | Description |
|---|---|
| `mp_hit_50px` | 1 if participant clicked within 50px of the target on the memory probe |
| `mp_target_correct` | 1 if participant clicked the correct target object |
| `mp_anchor_clicked` | 1 if participant clicked the valid anchor object |
| `dist_to_target_px` | Pixel distance from probe click to target center |

### anchor_rankings.csv
Row = one target object. Anchor objects ranked by their spatial predictiveness for each target.

| Column | Description |
|---|---|
| `target_name` | Target object name |
| `scene_type` / `scene_number` | Scene identifier |
| `1st_Anchor` – `4th_Anchor` | Anchor object names in rank order (1st = most predictive) |

### anchor_distribution.csv
Row = one target × anchor combination.

| Column | Description |
|---|---|
| `target_name` | Target object name |
| `valid_anchor` | Anchor object name |
| `n_first_anchor` | Number of times this anchor was selected as rank-1 across participants |

### scene_object_counts.csv
Row = one scene.

| Column | Description |
|---|---|
| `scene_type` / `scene_number` | Scene identifier |
| `total_visible_objects` | Total number of visible objects in the scene |

---

## Running the Analysis

### Requirements

- R (≥ 4.3.0)
- The following R packages:
  - `tidyverse`
  - `lme4`
  - `lmerTest`
  - `emmeans`
  - `coxme`
  - `survival`

Install all packages at once in R:
```r
install.packages(c("tidyverse", "lme4", "lmerTest", "emmeans", "coxme", "survival"))
```

### Steps

1. Clone or download this repository.
2. Open `Data and Analysis Code/etmsw_final_analyses.Rmd` in RStudio.
3. Set your working directory to the `Data and Analysis Code/` folder:
   ```r
   setwd("path/to/ProbAnchors_Materials/Data and Analysis Code")
   ```
4. Knit the document (click **Knit** in RStudio, or run `rmarkdown::render("etmsw_final_analyses.Rmd")`).

All analyses and figures in the paper will be reproduced in order.

---

## Running the Experiment

The experiment was programmed in Python using the SR Research EyeLink eye-tracking system.

### Requirements

- Python 3
- SR Research EyeLink Developer Kit (Pylink)
- A display connected to an EyeLink eye tracker

### Steps

1. Open `Experiment Code/etmsw_script_final.py`.
2. Ensure `trial_randomization_sheet.csv` is in the same directory as the script.
3. Place all stimuli images in the expected directory (see paths at the top of the script).
4. Run:
   ```bash
   python etmsw_script_final.py
   ```

---

## Contact

For questions about the data or code, please contact author.
