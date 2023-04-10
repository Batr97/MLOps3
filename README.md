# Batyrkhan_Gainitdinov

### Raised airflow locally using docker compose (taken from the example https://github.com/made-ml-in-prod-2021/airflow-examples /) 

### Implemented a dag that generates data for training the model, the DAG is called data_generation.py , some data is taken from my_config.yaml, which is located in the project/images/airflow-docker directory. It is important for you to simulate situations of constantly incoming data (5 points) data is recorded in project/data/raw/{{ds }}/data.csv and /data/raw/{{ds }}/target.csv

### Implemented a dag that trains the model weekly weekly_algorithm.py , using data for the current day. prepare training data (StandardScaler, train test split), read from /data/raw/{{ds }} and stored in /data/processed/{{ds }}/. 

### LogisticRegression is trained on train, save in /data/models/{{ds }}. The model is validated on val, classification-report is saved in /data/reports/{{ds }}. 

### Implemented a dag that uses the model daily daily_algorithm.py Used airflow variables (my_var, indicating the path to the model. The variable is set in docker-compose.yaml). Accepts data from point 1 as input. Makes predictions and writes them to /data/predictions/{{ds }}/predictions.csv. 

### As for DockerOperator, it is also implemented in the file daily_algorithm_dockerOp.py , all images are registered: airflow-preprocess, airflow-predict, airflow-predictions.