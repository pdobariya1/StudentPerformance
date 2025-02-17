# Student Performance Prediction

This project predicts a student's math score based on various factors like gender, ethnicity, parental education level, lunch type, test preparation course completion, reading score, and writing score.  The project is structured using a modular approach, separating data ingestion, transformation, model training, and prediction into distinct components.  A Flask web application provides a user interface for making predictions.

## Project Structure

* **`src`:** Contains the core Python code.
    * **`exception.py`:** Custom exception handling.
    * **`logger.py`:** Logging configuration.
    * **`utils.py`:** Utility functions for model evaluation, object saving/loading, etc.
    * **`components`:** Modules for data ingestion, transformation, and model training.
        * `data_ingestion.py`
        * `data_transformation.py`
        * `model_trainer.py`
    * **`pipeline`:** Contains the prediction pipeline.
        * `prediction_pipeline.py`
* **`templates`:** Contains HTML templates for the Flask web application.
    * `home.html`
    * `index.html`
* **`artifacts`:** Stores intermediate files like preprocessed data and the trained model.
* **`application.py`:** The Flask web application.
* **`main.py`:** Script to run the entire training pipeline offline.
* **`requirements.txt`:** Lists project dependencies.
* **`setup.py`:** For packaging the project.
* **`.ebextensions`:** Configuration for Elastic Beanstalk deployment (optional).


## Data

The project uses a dataset (presumably located in `notebook/data/stud.csv`) containing student performance information.  The training pipeline splits this data into training and testing sets, which are saved in the `artifacts` directory as `train.csv` and `test.csv`.


## Workflow

1. **Data Ingestion (`src/components/data_ingestion.py`):** Reads the dataset and splits it into training and testing sets.
2. **Data Transformation (`src/components/data_transformation.py`):** Preprocesses the data by handling missing values, scaling numerical features, and one-hot encoding categorical features. A preprocessor object is saved for later use in prediction.
3. **Model Training (`src/components/model_trainer.py`):** Trains multiple regression models (Random Forest, Decision Tree, Gradient Boosting, Linear Regression, K-Neighbors, XGBoost, CatBoost, AdaBoost) using `RandomizedSearchCV` for hyperparameter tuning. The best-performing model is selected and saved.
4. **Prediction (`src/pipeline/prediction_pipeline.py`):** Loads the saved model and preprocessor to make predictions on new data.


## Running the Project


1. **Clone the Repository:**
   ```bash
   git clone https://github.com/pdobariya1/StudentPerformance.git
   ```
2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
3. **Train the Model (Offline):** Run the training pipeline:
   ```bash
   python main.py
   ```
   This will create the `artifacts` directory and save the trained model and preprocessor.
4. **Run the Web Application:** Start the Flask app:
   ```bash
   python application.py
   ```
   Navigate to `http://127.0.0.1:5000/` (or `http://0.0.0.0:5000/` to allow external access) in your web browser to use the prediction interface.
