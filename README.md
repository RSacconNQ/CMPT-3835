# IFSSAA Client Retention Model

## Overview
This project aims to build a client retention model for the IFSSA food hamper distribution program. The model predicts whether a client will be retained ("Yes") or churned ("No") based on historical interaction data and environmental influences. The goal is to identify at-risk clients, allowing the program to tailor outreach strategies and services effectively.

## Features
The model utilizes the following engineered features:
1. **return_binary**: Target column indicating client return status within a 60-day window.
2. **days_since_last_pickup**: Tracks client interaction frequency.
3. **days_diff_scheduled_actual**: Measures service punctuality.
4. **rescheduled_flag**: Indicates if a pickup was rescheduled.
5. **month**: Captures seasonal trends.
6. **total_visits**: Sums visits per neighborhood.
7. **avg_days_between_pickups**: Calculates average gap between visits.
8. **is_single_pickup**: Flags clients with only one pickup.
9. **distance_to_center**: Measures distance from pickup location to client address.
10. **location_cluster**: Enables spatial analysis for resource optimization.

## Model Development
### Model Selection
Seven classification models were evaluated:
1. CatBoost
2. K-Nearest Neighbors (KNN)
3. Decision Tree
4. LightGBM
5. Random Forest
6. Gradient Boosting
7. XGBoost

### Best Performing Model
**CatBoost** achieved the highest F1-score of **0.9269** and was selected for further optimization.

### Hyperparameter Tuning
RandomizedSearchCV was used to fine-tune CatBoost, resulting in the following optimal parameters:
- 'classifier__learning_rate': 0.05500000000000001,
- 'classifier__l2_leaf_reg': 5,
- 'classifier__iterations': 1000,
- 'classifier__depth': 8

The tuned model achieved an F1-score of **0.9292** on the test set.

## Model Deployment
The model is deployed via a Streamlit web app, allowing users to input client details and receive predictions. The app includes:
- **Dashboard**: Overview and navigation.
- **Insights**: Exploratory data analysis and visualizations.
- **Predictions**: Interface for inputting client data and viewing predictions.

## Explainable AI (XAI)
SHAP (SHapley Additive exPlanations) was used to interpret the model's predictions, providing insights into feature importance and individual prediction explanations.

## Usage
### Prerequisites
- Python 3.11
- Libraries listed in `requirements.txt`

### Running the App
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Run the Streamlit app:
   ```bash
   streamlit run app.py
   ```

## Files
- `best_catboost_model.pkl`: Saved tuned CatBoost model.
- `model_top5.pkl`: Model trained on top 5 features.
- `feature_importances.csv`: Feature importance rankings.
- `app.py`: Streamlit application script.

## Results
- **Top Features**: `year_month_2024-08`, `total_visits`, `month`, `avg_days_between_pickups`, `Creator_(App admin)`.
- **Test Performance**:
  - Precision: 0.90
  - Recall: 0.97
  - F1-score: 0.93
  - ROC AUC: 0.91

## Contributors
- Chioma, Enkeshie, Renata and Ruth

## License
MIT

---

For detailed code and implementation, refer to the Jupyter notebook and scripts in the repository.
