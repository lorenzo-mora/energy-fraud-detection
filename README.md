# ![warning icon](warning.png) Energy Fraud Detection

An innovative and scalable system for automatic identification of energy fraud, based on the application of **AI** and **ML**, which aims at early detection of anomalous or suspicious behavior in energy consumption patterns. The ultimate goal is to <ins>prevent economic losses</ins> for electric utilities and <ins>ensure greater operational stability</ins> for the grid.

## Data
The data adopted for the preliminary feasibility phase were downloaded from [Kaggle](https://www.kaggle.com/datasets/taruneshburman/energy-fraud-detection). Through `kagglehub` it is possible to download the CSV file:
```python
import kagglehub

# Download latest version
path = kagglehub.dataset_download("taruneshburman/energy-fraud-detection")
```

The file is structured as follows:

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
