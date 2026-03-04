# AQI Simple Reflex Agent
A Simple Reflex Agent that reads environmental sensor data from a dataset and calculates the Air Quality Index (AQI) using pollutant concentration rules.

The agent processes hourly pollution measurements and determines:
- AQI value
- AQI category (Good, Satisfactory, Moderate, etc.)
- Dominant pollutant responsible for the AQI
- Health advisory message
The implementation follows the Simple Reflex Agent model from Artificial Intelligence, where the action depends only on the current percept (sensor readings).

## Agent Architecture
The system follows the Simple Reflex Agent model:

```
Environment (Air Quality Sensors / Dataset)
                ↓
Percept (Pollutant values)
                ↓
Rule Matching (AQI breakpoint rules)
                ↓
Action (Compute AQI)
                ↓
Output (AQI + Category + Dominant Pollutant)
```
## Dataset

Dataset used:
Air Quality Data in India (2015–2020)
https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india

Pollutants considered:
- PM2.5
- PM10
- SO₂
- NOx
- NH₃
- CO
- O₃

## Features
- Computes AQI using CPCB breakpoint formulas
- Handles rolling averages (24-hour and 8-hour windows)
- Detects dominant pollutant
- Handles missing data robustly
- Outputs AQI category and health message
- Works on large datasets (~30k rows)

  ## Running the Program
  ```
  python aqi_agent.py
  ```
  Just run the cell

## AQI Calculation Method

AQI is computed using sub-index interpolation for each pollutant.
General formula:
```
I = ((I_hi − I_lo) / (BP_hi − BP_lo)) * (C − BP_lo) + I_lo
```
I = AQI sub-index
C = pollutant concentration
BP = breakpoint concentration

## AQI Categories
| AQI Range | Category     |
| --------- | ------------ |
| 0-50      | Good         |
| 51-100    | Satisfactory |
| 101-200   | Moderate     |
| 201-300   | Poor         |
| 301-400   | Very Poor    |
| 401-500   | Severe       |

## Example Output
```
Total rows: 29971
Computed AQI rows: 27265
NaN AQI rows: 2706
```
Dominant Pollutants
```
NH3      18644
PM2.5     2875
CO        2194
SO2       2106
PM10       977
O3         435
NOx         33
```
Sample AQI Results
| Station | City               | DateTime         | AQI | Category     | Dominant Pollutant |
| ------- | ------------------ | ---------------- | --- | ------------ | ------------------ |
| KL007   | Thiruvananthapuram | 2020-02-14 08:00 | 66  | Satisfactory | PM10               |
| KL007   | Thiruvananthapuram | 2020-02-14 11:00 | 81  | Satisfactory | SO2                |
| KL007   | Thiruvananthapuram | 2020-02-14 15:00 | 105 | Moderate     | NH3                |



