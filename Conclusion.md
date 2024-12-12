# Conclusion

## Data Preparation

### Objectives

First, we took the data from the original CSV files. By filtering and extracting from raw data, we made sure only the needed parts were kept. Then, we cleaned and organized the data to make it ready for analysis and modeling.

---

## Data Exploration

### Objectives

In this step, we wanted to understand the data better using charts and basic statistics.

### Findings

1. **Crime Type Distribution**: Some crimes, like theft and battery, happen much more often than others. This shows we should focus on these common crimes for better predictions.

2. **Temporal Trends**: Crime rates change during the day, with higher rates in the evening. This means RNN could work well as suggested.

3. **Geographic Distribution**: Crimes are not spread evenly. Urban areas have more incidents. Adding location-based data could help improve accuracy.

4. **Data Quality Observations**: About 8% of the data is missing, though most of it is clean.

---

## Baseline Learning

### Methodology

We used past data to predict future crime patterns. Specifically, we looked at the crime types over the last 24 hours to predict the next hour. Batch learning was used to save memory while training the model.

### Results

- **Mean Squared Error (MSE)**: The model achieved an MSE of 1.562, showing it can make reasonable predictions.
- **Mean Percentage Error (MPE)**: The MPE was 54.80%, leaving room for improvement.

### Insights

The baseline model sets a starting point for comparing more complex models. While the MSE is low, the higher MPE shows that adding better features or techniques could help.

---

## Deep Learning

### Methodology

We used a Recurrent Neural Network (RNN) to model sequential crime data. The RNN processes time-series data to predict future crime patterns.

Key hyperparameters used:
- **Number of Layers**: 2
- **Hidden Size**: 64
- **Non-linearity**: ReLU
- **Dropout**: 0%
- **Batch Size**: 64
- **Optimizer**: Adam
- **Learning Rate**: 0.001

The RNN was trained on sequences of features (e.g., hour of day, crime type counts) and their associated labels (crime distributions in the next hour). A training-validation-test split was used to evaluate the model's performance.

### Results

- **Validation Loss**: The model's validation loss decreased consistently over 20 epochs, reaching a minimum of **1.2447**.
- **Test Loss**: The model achieved a test loss of **1.26** and an RMSE of **1.12**.
- **Mean Percentage Error (MPE)**: The overall MPE was **85.79%**, indicating room for improvement in model accuracy.

### Insights

The RNN performed well in capturing temporal patterns in crime data but struggled with certain crime categories, as seen in the high percentage error for some labels. Fine-tuning hyperparameters or exploring advanced architectures like LSTMs or GRUs could further enhance performance. Adding more representative features might also reduce errors.

---

## Feature Importance

### Objectives

We wanted to figure out which features matter most for making good predictions.

### Key Steps

1. **Feature Grouping**: We grouped features by type, like time-based or crime-based features.

2. **Permutation Importance**: We shuffled the data for specific features to see how much worse the model got, measuring their importance.

3. **Evaluation**: We calculated scores for each feature group to see which ones were most helpful.

### Findings

1. **Hour of Day**: This was the most important feature, scoring **10.62**. It shows clear patterns of crimes happening at different times of the day.

2. **Crime Type Features** (`feature_num_crime`): These scored **4.29**, making them important for predicting future crimes.

3. **Yearly Temporal Features** (`feature_year`): Scored **3.70**, showing seasonal trends also matter.

4. **Arrest Percentage**: Scored **1.28**, having some impact but less than others.

5. **Day of Week** and **Month of Year**: Scored **0.86** and **0.52**, meaning they have a smaller role in predictions.

6. **Week of Year**: Scored **0.40**, making it the least helpful feature.

### Insights

The `Hour of Day` feature stands out as the most useful for predicting crimes. It matches well with observed daily crime patterns. Other features like `Crime Type` and `Yearly Trends` also add value, but features like `Week of Year` and `Day of Week` might not be as helpful.

Improving the weaker features or creating new ones could boost future model accuracy. Focusing on key time-based and categorical features is essential for better predictions.

---

