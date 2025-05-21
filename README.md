
# End-to-End AI Solution with PySpark & Real-Time Data Processing Using Apache NiFi

This project demonstrates an end-to-end AI pipeline that includes real-time data ingestion, transformation, and analytics using Apache NiFi and PySpark. The solution is deployed on Google Cloud Platform and consists of two key phases:

1. **Real-Time Data Collection and Transformation**  
   Data is ingested in real-time using the **NGSI-LD Context Broker**, then transformed and persisted via **DRACO**, a FIWARE component built on **Apache NiFi**.

2. **AI Modeling with PySpark on Google Cloud Dataproc**  
   Apache Spark is used to process data and build machine learning models using PySpark and **Spark MLlib**. The entire development process is facilitated via **Jupyter Notebooks** on a **Google Cloud Dataproc** cluster.

---

## 📌 Project Agenda
- General Architecture Overview  
- Technologies Used  
- Setting Up the Cloud Environment  
- Running the AI Pipeline  

---

## 🧭 General Architecture
The architecture follows a modular, cloud-native design. Real-time data flows through FIWARE components (NGSI-LD, DRACO), is persisted, and then analyzed on Dataproc using Spark. JupyterLab serves as the interactive front-end for model development.

---

## 🛠 Technologies Used

- **NGSI-LD Context Broker**:  
  A FIWARE Generic Enabler for real-time context data management. Supports updates, queries, registrations, and subscriptions for contextual information.

- **DRACO (Apache NiFi)**:  
  Manages historical data flow and transformation using Apache NiFi. Offers scalable, flow-based programming for automating complex data pipelines.

- **Apache NiFi**:  
  Core technology behind DRACO, providing a powerful interface for creating data flow pipelines.

- **Google Cloud Dataproc**:  
  A managed Spark and Hadoop service that simplifies running large-scale data processing and ML workloads.

- **PySpark**:  
  Python interface for Apache Spark that supports Spark SQL, Streaming, DataFrames, and MLlib.

- **Spark MLlib**:  
  Spark's machine learning library used to develop scalable ML pipelines.

- **Jupyter Notebook**:  
  Interactive environment for building and executing PySpark code, visualizing data, and documenting the process.

---

## ☁️ Cloud Environment Setup (Google Cloud Platform)

Follow these steps to set up your GCP environment:

### Step 1: Create a Google Cloud Project

- Go to: [Google Cloud Console](https://console.cloud.google.com)  
- Create a new project

Enable required APIs via Cloud Shell:
```bash
$ gcloud config set project <PROJECT_ID>

$ gcloud services enable dataproc.googleapis.com \
    compute.googleapis.com \
    storage-component.googleapis.com
```

### Step 2: Create a Cloud Storage Bucket

Create a uniquely named bucket in a region close to your data:

- Open **Cloud Storage** in GCP Console  
- Click **“Create bucket”** and follow the form instructions

### Step 3: Create a Dataproc Cluster with Jupyter & Component Gateway

You can create the cluster using either the UI or the Cloud Shell:

```bash
$ gcloud beta dataproc clusters create ${CLUSTER_NAME} \
  --region=${REGION} \
  --image-version=1.4 \
  --master-machine-type=n1-standard-4 \
  --worker-machine-type=n1-standard-4 \
  --bucket=${BUCKET_NAME} \
  --optional-components=ANACONDA,JUPYTER \
  --enable-component-gateway
```

> ℹ️ By default, the cluster will include 1 master and 2 worker nodes. You can customize node types and counts as needed.

### Step 4: Access the JupyterLab Web Interface

- Go to **Dataproc > Clusters**  
- Click your cluster name  
- Navigate to the **“Web Interfaces”** tab  
- Click the **JupyterLab** link via the **Component Gateway**

### Step 5: Create a PySpark Notebook for the AI Solution

- Use **Python 3** kernel (with Anaconda and PySpark pre-installed)
- You can configure a `SparkSession` and use Google Cloud APIs such as BigQuery within the notebook

> 💡 It's best to create a dedicated folder in your GCS bucket where notebooks will be stored.

---

## 📂 Additional Resources

For more information regarding:
- Real-time data ingestion and NiFi workflows → check the **DRACO/NiFi folder**  
- AI modeling and PySpark implementation → check the **PySpark folder**
