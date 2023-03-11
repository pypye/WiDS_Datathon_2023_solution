# WiDS Datathon 2023 13th Place Solution
We are **UET 杨蓉** who achieved **13th place** in [WiDS Global](https://www.kaggle.com/competitions/widsdatathon2023) and **1st place** in [WiDS Hanoi](https://www.facebook.com/WiDSVietNam). The below write-up demonstrate our performance in the WiDS competition.

# Pre-processing
- Removed all of the physical model forecast features, including word "prate", "tmp2m".
- After that extract feature using CatBoost feature importance.
![image](https://user-images.githubusercontent.com/69345080/224473620-cb3d5068-e5b3-4023-b4b9-66cf87866dfb.png)

# Train/Validation Strategy
- We use K-Fold for train/validation strategy with ``K=5``

# Model
- We train the dataset using CatBoost model with below hyper parameters:
```py
{ 
      'iterations': 24000,
      'learning_rate' : 0.1,
      'subsample' : 0.75, 
      'max_depth’ : 6,
      'use_best_model' : True, 
      'loss_function' : 'RMSE'
}
```
- The result in LB is **0.729 RMSE**.

# Post-processing
- Given that the train dataset time occurs during the El Nino phase, the temperature is above average. The test dataset time occurs during the La Nina phase, so the temperature is higher than usual. The predicted temperature will be higher, which is obvious.
- Accordingly, we adjust the temperature based on report from [Western Regional Climate Center](https://www.wrcc.dri.edu/Climate/Monthly_Summaries/west_summaries.php).
- The final result in LB is **0.693 RMSE**.
