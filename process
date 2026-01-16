import os
import json
import logging
from datetime import datetime
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
logging.basicConfig(level=logging.INFO,format="%(asctime)s - %(levelname)s - %(message)s")
CONFIG = {"input_path": "./data/raw","output_path": "./data/processed","numeric_features": ["age", "income", "score"],"categorical_features": ["gender", "education", "region"],"drop_features": ["id", "notes"]}
class ETLPipeline:
    def __init__(self, config):
        self.config = config
        self.df = None
        self.processed_df = None
    def extract(self, file_name):
        path = os.path.join(self.config["input_path"], file_name)
        self.df = pd.read_csv(path)
        logging.info(f"[EXTRACT] Data loaded with shape {self.df.shape}")
        return self
    def explore(self):
        logging.info("[EXPLORE] Missing values summary")
        logging.info(f"\n{self.df.isnull().sum()}")
        return self
    def validate(self):
        if (self.df['age'] <= 0).any():
            raise ValueError("Invalid age values detected")
        if (self.df['income'] <= 0).any():
            raise ValueError("Invalid income values detected")
        logging.info("[VALIDATE] Data validation passed")
        return self
    def feature_engineering(self):
        self.df['income_per_age'] = self.df['income'] / self.df['age']
        self.df['high_income'] = (self.df['income'] > 100000).astype(int)
        logging.info("[FEATURE ENGINEERING] New features created")
        return self
    def transform(self):
        X = self.df.drop(columns=self.config['drop_features'])
        numeric_pipeline = Pipeline([('scaler', StandardScaler())])
        categorical_pipeline = Pipeline([('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))])
        preprocessor = ColumnTransformer([('num', numeric_pipeline, self.config['numeric_features']),('cat', categorical_pipeline, self.config['categorical_features'])])
        transformed_array = preprocessor.fit_transform(X)
        feature_names = (self.config['numeric_features'] +list(preprocessor.named_transformers_['cat'].named_steps['encoder'].get_feature_names_out(self.config['categorical_features']) ))
        self.processed_df = pd.DataFrame(transformed_array, columns=feature_names)
        logging.info(f"[TRANSFORM] Data transformed: {self.processed_df.shape}")
        return self
    def load(self, file_name):
        os.makedirs(self.config['output_path'], exist_ok=True)
        path = os.path.join(self.config['output_path'], file_name)
        self.processed_df.to_csv(path, index=False)
        logging.info(f"[LOAD] Processed data saved to {path}")
        return self
    def report(self):
        report_data = {"rows": int(self.processed_df.shape[0]),"columns": int(self.processed_df.shape[1]),"generated_on": datetime.now().strftime("%Y-%m-%d %H:%M:%S") }
        report_path = os.path.join(self.config['output_path'], "report.json")
        with open(report_path, 'w') as f:
            json.dump(report_data, f, indent=4)
        logging.info(f"[REPORT] Report generated at {report_path}")
        return self
def generate_sample_data():
    os.makedirs("./data/raw", exist_ok=True)
    df = pd.DataFrame({'id': range(1, 101),'age': np.random.randint(18, 65, 100),'income': np.random.randint(30000, 150000, 100),'score': np.random.randint(1, 100, 100),'gender': np.random.choice(['M', 'F'], 100),'education': np.random.choice(['High School', 'Bachelor', 'Master', 'PhD'], 100),'region': np.random.choice(['North', 'South', 'East', 'West'], 100),'notes': ['Note ' + str(i) for i in range(1, 101)]})
    df.to_csv("./data/raw/sample_data.csv", index=False)
    logging.info("[DATA] Sample data generated")
if __name__ == "__main__":
    generate_sample_data()
    pipeline = ETLPipeline(CONFIG) 
    pipeline.extract("sample_data.csv") \
        .explore() \
            .validate() \
                .feature_engineering() \
                    .transform() \
                          .load("processed_data.csv") \
                            .report() 
    logging.info("ETL Pipeline executed successfully")
