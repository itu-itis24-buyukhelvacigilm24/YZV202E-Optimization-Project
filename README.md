# YZV202E Optimization Project

## Istanbul Emergency Logistics Hub

This notebook studies where a single emergency logistics hub could be placed in Istanbul.

The idea is to place the hub close to important health facilities. Districts with higher earthquake risk are given higher weights.

## Files

- `Emergency_Logistics_Hub_Optimization.ipynb`: main notebook
- `data/`: input datasets
- `outputs/`: figures, result tables, and map output
- `requirements.txt`: required Python packages

## Data

Two IBB Open Data Portal datasets are used:

- Health facilities: https://data.ibb.gov.tr/dataset/istanbul-saglik-kurum-ve-kuruluslari-verisi
- Earthquake scenario results: https://data.ibb.gov.tr/dataset/deprem-senaryosu-analiz-sonuclari

The health dataset has many categories. Some of them are not useful for this problem, such as pharmacies, dentists, opticians, and medical stores. The notebook filters the data and keeps more relevant categories like hospitals, polyclinics, family health centers, emergency stations, and dialysis centers.

## Method

The model minimizes weighted Haversine distance.

Main steps:

1. Read the two datasets.
2. Check health facility categories.
3. Filter facilities for emergency response.
4. Create a district risk score from earthquake scenario data.
5. Merge facility data with district risk weights.
6. Use SciPy optimization methods to find the hub location.
7. Plot the result and create an Istanbul map.

Methods compared:

- L-BFGS-B
- Powell
- Nelder-Mead

The notebook also includes an `n` slider. It changes how many top weighted facilities are used.

## Notes

Haversine distance is used because the data is latitude-longitude based.

The model uses a small epsilon value in the distance formula. This avoids numerical problems when the candidate hub is very close to a facility coordinate.

The final hub point is only a model result. A real location decision would also need road access, land use, and sea/land checks.

## Run

```bash
pip install -r requirements.txt
jupyter notebook Emergency_Logistics_Hub_Optimization.ipynb
```

## Outputs

Some output files:

- `outputs/optimized_hub_map.png`
- `outputs/istanbul_hub_map.html`
- `outputs/top_district_risk.png`
- `outputs/method_comparison.png`
- `outputs/n_sensitivity.png`
