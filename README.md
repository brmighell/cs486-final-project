# Recidivism Risk Predictor 

## Repo Structure
```
|COMPAS
|  |logs/hparam_tuning
|  |COMPAS_model.ipynb
|  |compas_people.csv
|
|COMPAS_no_race
|  |logs/hparam_tuning
|  |COMPAS_no_race.ipynb
|  |compas_people.csv
|
|Iowa
|  |logs/hparam_tuning
|  |3_year_recidivism_elaborated_2.csv
|  |Iowa_model.ipynb
|
|Iowa_no_race
|  |logs/hparam_tuning
|  |3_year_recidivism_elaborated_2.csv
|  |Iowa_no_race.ipynb
```

## Notable Files:
- `COMPAS_model.ipynb` - This Jupyter Notebook file contains all modelling done on `compas_people.csv` as well as a brief analysis of results at the bottom.
- `COMPAS_no_race.ipynb` - Same as above just with all ethnic features removed.
- `compas_people.csv` - This dataset is taken from a repo created by the authors of a ProPublica study of racism in recidivist algorithms. Source: https://github.com/propublica/compas-analysis/blob/master/compas.db
- `3_year_recidivism_elaborated_2.csv` - A Kaggle dataset referencing a 3-year period of recidivism in Iowa. Source: https://www.kaggle.com/kerneler/starter-3-year-recidivism-2747e192-0/data
- `Iowa_model.ipynb` - This Jupyter Notebook file contains all modelling done on `3_year_recidivism_elaborated_2.csv` as well as a brief analysis of results at the bottom.
- `Iowa_no_race.ipynb` - Same as above just with all ethnic features removed.

## Process Overview:
We analyzed and trained models (using a variety of algorithms) on both datasets, selecting the model with the best performance to finally validate. Interestingly, no one model is far and away better than the others.

|  | `best_model` Accuracy Score |
|--|--|
| COMPAS | 0.717 |
| COMPAS_no_race | 0.716 |
| Iowa | 0.680 |
| Iowa_no_race | 0.672 |

Each folder is fully self-contained and can be run independently of the other.

## Brief Thoughts:
Both of the models for the Iowa and COMPAS datasets wound up slightly racist, though in opposite directions. Here's a table showing how the COMPAS model was more likely to assign false positives to African-Americans while the Iowa model was more likely to incorrectly flag Caucasians.
___

|  | Caucasian | African-American |
|--|--|--|
| COMPAS | -12.25% | +18.38% |
| COMPAS_no_race | -8.67% | +9.94% |
| Iowa | +12.29% | -7.18% |
| Iowa_no_race | +1.18% | -1.13% |

___

Interestingly, when fitting for COMPAS, DNN models' racism seemed to be proportional to the number of epochs. That is, the higher the number of epochs the more racist the model.

Also worth noting is that, when race was removed as a feature, both models' racism dropped although the model trained on the COMPAS dataset didn't drop nearly as sharply as the Iowa model. Accuracy dropped as well though, on the plus side, not by a whole lot.

## Closing Thoughts
- Could possibly include racism as a filtering factor for `best_model` instead of only going by accuracy.
- 

## Notes:
- As-is the DNN models include functionality to write run logs to whatever machine they're running on.
- Each notebook uses TensorBoard to display various information about the DNN models created. It's pretty neat and ultimately not essential to understanding the model itself.
