# Data

This project uses **CGMacros: a scientific dataset for personalized nutrition and diet monitoring (v1.0.0)**, available on PhysioNet:

https://physionet.org/content/cgmacros/1.0.0/

The data is not included in this repository. It is open access (no credentialing required) and licensed under **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 (CC BY-NC-SA 4.0)**: credit the dataset, use it non-commercially, and share any derived data under the same license.

## Getting it

1. Download `CGMacros_dateshifted365.zip` (about 650 MB) from the "Files" section of the PhysioNet page.
2. Extract it. You'll get a `CGMacros` folder containing:
   - one folder per participant (`CGMacros-001` … `CGMacros-049`, 45 participants), each with a minute-level CSV and meal photos
   - `bio.csv` (demographics and lab tests), `gut_health_test.csv`, `microbes.csv`
3. Copy the three notebooks from `notebooks/` into that `CGMacros` folder and run them in order.

## What the notebooks create

Running the notebooks creates a `processed/` folder inside `CGMacros`:

| File | Created by | Contents |
|---|---|---|
| `dexcom_5min.csv` | EDA | Dexcom glucose at its native 5-minute rate |
| `meals_clean.csv` | EDA | Meals with impossible values removed and labels normalized |
| `meal_responses.csv` | EDA | One row per isolated meal: rise, time to peak, iAUC, activity |
| `participants.csv`, `participant_flags.csv` | EDA | Per-person demographics, coverage, sensor agreement and data-quality flags |
| `unlogged_rises.csv` | EDA | Glucose rises with no logged meal |
| `model1_*.csv` | Modeling_1 | Physics-model parameters and test scores |
| `pinn_*.csv`, `pinn_hybrid_model.pt` | PINN_modeling | Hybrid-model scores, person parameters and trained model |

These files are derived from CGMacros, so they fall under the same CC BY-NC-SA 4.0 license if shared.

## Notes on the data

- Timestamps are date-shifted for privacy; time of day is preserved.
- Glucose values in the CSVs are interpolated to one-minute resolution; the sensors' real rates are 5 minutes (Dexcom) and 15 minutes (Libre).
- Activity is recorded as METs for most participants and as a 0–3 intensity level for others; the EDA harmonizes both.
