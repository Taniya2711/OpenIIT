
# Flight Delay Prediction and Rescheduling Optimization

## Project Overview

This project develops a machine learning-based framework for predicting flight delays and optimizing flight schedules to minimize cumulative arrival delays.

Using a dataset of approximately 3 million flight records, the project combines data preprocessing, feature engineering, predictive modelling, and Genetic Algorithm-based optimization to investigate the impact of flight rescheduling on overall delay reduction.

The framework integrates XGBoost, CatBoost, and LSTM-based predictive approaches with an evolutionary optimization algorithm to generate improved flight departure schedules.

## Objectives

- Predict flight delays using historical flight and operational data.
- Identify important temporal and operational factors influencing flight delays.
- Compare machine learning models for delay prediction.
- Develop a Genetic Algorithm for flight rescheduling.
- Minimize cumulative predicted arrival delays while maintaining feasible flight schedules.

## Dataset

The project uses a large-scale flight dataset containing approximately 3 million records.

Key features include:

- **Flight Information:** Airline, origin airport, destination airport, and flight number.
- **Temporal Features:** Scheduled departure and arrival times, flight date, year, month, and day.
- **Operational Features:** Flight distance, taxi-in time, and taxi-out time.
- **Target Variables:** Delay components associated with carrier, weather, security, National Airspace System (NAS), and late-arriving aircraft.

The delay components are used to model different sources of flight delays and support overall arrival-delay prediction.

## Methodology

### 1. Data Preprocessing and Feature Engineering

- Processed approximately 3 million flight records and curated valid delay-reason observations.
- Converted scheduled departure and arrival times into minutes past midnight for easier numerical modelling.
- Extracted year, month, and day features from flight dates.
- Processed numerical and categorical variables, including airline, origin, destination, distance, and taxi times.
- Prepared separate target variables for delay components and overall arrival delay.
- Investigated Principal Component Analysis (PCA) on numerical features; it did not provide meaningful improvement and was not retained in the final modelling workflow.

### 2. Flight Delay Prediction

Implemented and evaluated machine learning models to predict flight delays using historical flight information.

#### XGBoost

- Trained XGBoost regression models to predict flight delay components.
- Evaluated performance using Mean Absolute Error (MAE) and Mean Squared Error (MSE).
- Applied RandomizedSearchCV for hyperparameter tuning using three-fold cross-validation and 50 parameter configurations.
- Analysed feature importance to identify influential predictors.

#### CatBoost

- Evaluated CatBoost as an additional gradient-boosting approach for flight-delay prediction.
- Compared its predictive performance with other machine learning models.

#### LSTM

- Developed an LSTM-based architecture for multi-output flight-delay prediction.
- Incorporated embedding layers for categorical features such as airline, origin, and destination.
- Combined categorical embeddings with numerical flight features.
- Used an LSTM layer and a dense output layer to predict five delay components.
- Evaluated predictions using MAE and MSE.

### 3. Flight Rescheduling Using Genetic Algorithm

Designed a Genetic Algorithm to optimize flight departure schedules based on predicted delays.

The optimization framework uses predicted arrival delays from the trained XGBoost model to evaluate alternative departure schedules.

#### Genetic Algorithm Configuration

- Population size: 30
- Number of generations: 100
- Mutation rate: 0.1
- Tournament selection size: 5

#### Optimization Process

1. Selected a set of flights for rescheduling.
2. Represented candidate solutions using revised scheduled departure times.
3. Evaluated each candidate using a fitness function based on total predicted arrival delay.
4. Incorporated penalties for violations of minimum turnaround-time requirements.
5. Applied selection, crossover, and mutation to evolve candidate schedules.
6. Enforced minimum turnaround buffers between consecutive flights operated by the same airline.
7. Repeated the optimization process over 100 generations to identify improved schedules.

The objective was to reduce cumulative predicted arrival delays while maintaining operational feasibility.

## Results

- **Dataset Scale:** Approximately 3 million flight records used for predictive modelling.
- **XGBoost Performance:** Achieved an MAE of 9.5 minutes for flight-delay prediction.
- **Rescheduling Optimization:** Reduced cumulative delay by 18% over 100 Genetic Algorithm generations.

The results demonstrate the potential of combining machine learning-based delay prediction with evolutionary optimization for flight schedule improvement.

## Technologies Used

- **Programming Language:** Python
- **Data Processing:** Pandas, NumPy
- **Machine Learning:** XGBoost, CatBoost, Scikit-learn
- **Deep Learning:** TensorFlow, Keras, LSTM
- **Optimization:** Genetic Algorithm
- **Visualization:** Matplotlib, Seaborn, Plotly
- **Environment:** Jupyter Notebook, Google Colab

## Repository Structure

```text
Flight-Delay-Optimization/
│
├── OpenIIT.ipynb
└── README.md
```

## How to Run

### Prerequisites

Install the required libraries:

```bash
pip install numpy pandas matplotlib seaborn plotly
pip install scikit-learn xgboost catboost
pip install tensorflow
```

### Execution

1. Open `OpenIIT.ipynb` in Jupyter Notebook or Google Colab.
2. Load the required flight dataset.
3. Execute the preprocessing and feature engineering cells.
4. Train and evaluate the delay prediction models.
5. Run the Genetic Algorithm-based rescheduling workflow.
6. Review the predicted delays, optimized schedules, and evaluation results.

## Future Scope

- Incorporate additional operational constraints, including airport capacity and aircraft availability.
- Extend the rescheduling framework to account for connecting flights and network-wide delay propagation.
- Explore more advanced sequence-based architectures for capturing temporal dependencies.
- Evaluate optimization performance across multiple days and larger flight networks.
- Investigate multi-objective optimization balancing delay reduction, operational costs, and schedule stability.

## Acknowledgements

Developed as part of **Open IIT – Data Analytics**, IIT Kharagpur.
