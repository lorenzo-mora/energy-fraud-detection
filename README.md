# ![warning icon](warning.png) Energy Fraud Detection

An innovative and scalable system for automatic identification of energy fraud, based on the application of **AI** and **ML**, which aims at early detection of anomalous or suspicious behavior in energy consumption patterns. The ultimate goal is to <ins>prevent economic losses</ins> for electric utilities and <ins>ensure greater operational stability</ins> for the grid.

## Data
The data adopted for the preliminary feasibility phase were downloaded from [Kaggle](https://www.kaggle.com/datasets/) via `kagglehub`. Three different datasets were adopted for this first phase.

### 1. [__Energy Fraud Detection__](https://www.kaggle.com/datasets/taruneshburman/energy-fraud-detection) by Tarunesh Burman
The dataset can be downloaded as follows:
```python
import kagglehub
path = kagglehub.dataset_download("taruneshburman/energy-fraud-detection")
```

The file `Energy_Fraud_Detection.csv` is structured as follows:

| Column Name                | Data Type                                                   | Description                                                     |
|----------------------------|-------------------------------------------------------------|-----------------------------------------------------------------|
| `Customer_Type`            | _Literal[`Residential`, `Commercial`]_                      | Customer type                                                   |
| `Average_Bill_Amount`      | _float_                                                     | Average monthly bill amount in dollars                          |
| `Meter_Readings_Deviation` | _float_                                                     | Percentage deviation of meter readings from expected values     |
| `Billing_Cycle`            | _Literal[`Monthly`, `Quarterly`]_                           | Type of billing cycle                                           |
| `Historical_Consumption`   | _float_                                                     | Historical average energy consumption in kW/h                   |
| `Meter_Type`               | _Literal[`Digital`, `Analog`]_                              | Type of energy meter used                                       |
| `Tampering_Alerts`         | _float_                                                     | Number of warnings indicating potential meter tampering         |
| `Last_Inspection_Days`     | _float_                                                     | Number of days since the last meter inspection                  |
| `Peak_Usage_Anomalies`     | _float_                                                     | Number of anomalies detected during peak usage hours            |
| `Complaints_Logged`        | _float_                                                     | Number of billing-related complaints registered by the customer |
| `Fraud_Status`             | _Literal[`No Fraud`, `Potential Fraud`, `Confirmed Fraud`]_ | Target variable classifying fraud status                        |

After an initial analysis, which can be found in [`burman.ipynb`](eda/burman.ipynb), it emerged that the available instances (1000 distinct invoices) could be filtered by removing the _analogue PODs_ and divided according to the two types of customer present.
However, the two groups thus generated consisted of 269 (_residential_ customers) and 268 instances (_business_ customers) respectively. For this reason, the trainings conducted in the same file were found to be insufficiently accurate.

### 2. [__Fraud Detection in Electricity and Gas Consumption__](https://www.kaggle.com/datasets/mrmorj/fraud-detection-in-electricity-and-gas-consumption) by Andrii Samoshyn
The dataset can be downloaded as follows:
```python
import kagglehub
path = kagglehub.dataset_download("mrmorj/fraud-detection-in-electricity-and-gas-consumption")
```

The dataset consists of the files:
* `client_train.csv`
* `invoice_train.csv`
* `client_test.csv`
* `invoice_test.csv`

where the CSVs relating to invoices are structured as follows:

| Column Name            | Data Type                | Description                                                            |
|------------------------|--------------------------|------------------------------------------------------------------------|
| `client_id`            | _str_                    | Unique id for the client                                               |
| `invoice_date`         | _str_                    | Date of the invoice                                                    |
| `tarif_type`           | _int_                    | Type of tax                                                            |
| `counter_number`       | _int_                    | Meter identification number                                            |
| `counter_statue`       | __???__                  | __???__                                                                |
| `counter_code`         | _int_                    | Meter code                                                             |
| `reading_remarque`     | _int_                    | Notes taken during the STEG agent's visit to the customer              |
| `counter_coefficient`  | _int_                    | Additional coefficient to be added if standard consumption is exceeded |
| `consommation_level_1` | _int_                    | Consumption level 1                                                    |
| `consommation_level_2` | _int_                    | Consumption level 2                                                    |
| `consommation_level_3` | _int_                    | Consumption level 3                                                    |
| `consommation_level_4` | _int_                    | Consumption level 4                                                    |
| `old_index`            | _int_                    | Old index                                                              |
| `new_index`            | _int_                    | New index                                                              |
| `months_number`        | _int_                    | Number of the month                                                    |
| `counter_type`         | _Literal[`ELEC`, `GAZ`]_ | Type of the meter                                                      |

whereas the CSVs relating to customers are structured as follows:

| Column Name     | Data Type      | Description                                                    |
|-----------------|----------------|----------------------------------------------------------------|
| `district`      | _int_          | District in which the client is located                        |
| `client_id`     | _str_          | Unique id for the client                                       |
| `client_catg`   | _int_          | Customer category                                              |
| `region`        | _int_          | Area where the customer is located                             |
| `creation_date` | _str_          | Date of customer joining                                       |

For the latter type of table, the training set (`client_train.csv`) also has the `taregt` column, which is the variable that classifies the fraud status and takes the values 0 (non-fraudulent customer) or 1 (fraudulent customer).

The analyses conducted on this dataset are collected in [`samoshyn.ipynb`](eda/samoshyn.ipynb).

### 3. [__Electricity Theft Detection__](https://github.com/henryRDlab/ElectricityTheftDetection) by Zibin Zheng
The dataset can be downloaded directly from [GitHub](https://github.com/henryRDlab/ElectricityTheftDetection) and then unzipped (as specified [here](https://github.com/henryRDlab/ElectricityTheftDetection/issues/1#issuecomment-2060104395)).

The `data.csv` in which the data is collected presents for each line the daily consumption of the respective POD (42'372) from 1 January 2014 to 31 October 2016. Each POD is also associated with a label (`FLAG`) that identifies a fraudulent user (`1`) from a non-fraudulent one (`0`).

> From an in-depth initial analysis, the data seem to have interesting potential as a basis for the implementation of models. However, compatibility with energy consumption data other than Chinese consumers (such as Italian consumers) must be verified.<br>The analyses are collected in [`zheng.ipynb`](eda/zheng.ipynb).