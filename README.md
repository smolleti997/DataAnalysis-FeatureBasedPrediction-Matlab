
# CGM & Insulin Data Analysis and Feature-Based Prediction in MATLAB

**Description:**
This MATLAB project processes **Continuous Glucose Monitoring (CGM)** and **insulin pump data** to compute glucose metrics, extract features, perform clustering, and predict glucose-related outcomes. The workflow includes **data preprocessing, meal detection, feature extraction, machine learning predictions, and clustering evaluation**.

---

## **Features**

1. **CGM & Insulin Data Analysis**

   * Reads CGM and insulin CSV files (`CGMData.csv`, `InsulinData.csv`)
   * Interpolates missing CGM readings
   * Combines date and time into a single datetime column
   * Separates **auto** and **manual insulin pump modes**
   * Computes glucose metrics for **day (6–23 h)**, **night (0–6 h)**, and **whole day (0–23 h)**
   * Calculates **time-in-range percentages** for each mode
   * Saves results to `Results.csv`

2. **Feature Extraction & Prediction**

   * Reads **test data** (`test.csv`)
   * Computes **moving window means** of CGM data
   * Calculates **CGM amplitude** (`max - min`)
   * Extracts **FFT features** (frequency-domain)
   * Constructs a **feature matrix** and predicts outcomes using a **pre-trained model** (`trainedModel`)
   * Saves predictions to `Results1.csv`

3. **Ground Truth & Meal Feature Extraction**

   * Reads insulin data for **meal times** (`InsulinData.csv`)
   * Cleans meal values and bins carb intake into ranges
   * Aligns meal start times with CGM data
   * Constructs a **meal feature matrix** (`Groundtruth` / `mealdatamatrix`)
   * Extracts **windowed mean, amplitude, FFT, velocity, and acceleration features** for meals
   * Performs **clustering** using **k-means** and **DBSCAN**
   * Calculates **SSE, entropy, and purity** for clustering evaluation
   * Saves clustering results to `Results_hw3.csv`

---

## **Workflow**

### **1. CGM & Insulin Data Analysis**

1. Import CGM and insulin CSV files.
2. Interpolate missing CGM readings.
3. Merge date and time into a single datetime column.
4. Separate **auto** and **manual mode** periods.
5. Compute glucose metrics for **day**, **night**, and **whole day**.
6. Calculate **time-in-range percentages**.
7. Save results in `Results.csv`.

---

### **2. Feature Extraction & Testing**

1. Read the test CSV file.
2. Compute **moving window mean features**.
3. Calculate **CGM amplitude** for each row (`max - min`).
4. Compute **FFT features** to capture frequency characteristics.
5. Combine all features into a **feature matrix**.
6. Predict outcomes using a **trained model**:

   ```matlab
   yfit = trainedModel.predictFcn(testfeaturematrix);
   ```
7. Save predictions to `Results1.csv`.

---

### **3. Ground Truth & Meal Feature Extraction**

1. Read insulin CSV and extract **meal values**.
2. Bin meal values based on carb ranges.
3. Align meal times with CGM readings.
4. Construct **meal feature matrix** for analysis.
5. Extract features:

   * Moving window mean (6 features)
   * CGM amplitude
   * FFT-based features (3 features)
   * CGM velocity & acceleration
6. Perform **clustering**:

   * K-means (7 clusters)
   * DBSCAN
7. Compute clustering evaluation metrics: **SSE, entropy, purity**
8. Save results to `Results_hw3.csv`.

---

## **Dependencies**

* MATLAB R2020a or later
* CSV files: `InsulinData.csv`, `CGMData.csv`, `test.csv`
* Pre-trained model: `trainedModel.mat`

---

## **Outputs**

* `Results.csv` – CGM time-in-range and glucose metrics
* `Results1.csv` – Predicted outcomes for test dataset
* `Results_hw3.csv` – Clustering evaluation metrics

---

## **Future Improvements**

* Visualization for CGM metrics, predictions, and clusters
* Automate multiple patient dataset processing
* Optimize FFT and moving window computations for speed
* Build a GUI for uploading test files and visualizing results

