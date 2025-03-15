# Quadruple Tank Level System - Process Identification

## Project Overview 

This repository contains the project "Quadruple Tank Level System Data-Driven Process Identification" conducted as part of CHE 662 - Process Identification at the University. The project focuses on identifying a Multiple Input Multiple Output (MIMO) system using various parametric and non-parametric methods.

## Introduction
The study focuses on quadruple tank level systems with two pumps (left and right) controlling water flow rates into two bottom tanks. The system is analyzed as two Multiple Input Single Output (MISO) processes:
MISO Model Z_L: Bottom Left Tank (Y1) with inputs Left Pump (U1) & Right Pump (U2)
MISO Model Z_R: Bottom Right Tank (Y2) with inputs Left Pump (U1) & Right Pump (U2)
Various system identification techniques were employed, including parametric models (ARX, ARMAX, BJ, OE), non-linear models, and subspace models. Additionally, an LSTM-based neural network was implemented to compare its performance.

## Methodology
1. Data Extraction
Step test performed from steady-state flow rate 12 L/min to 14 L/min for each pump.
RBS signal generated using MATLAB’s idinput function.
2. Random Binary Sequence (RBS) Signal Design

|       Parameter          		| Value |   Criteria 			 | 
|-------------------------------| ----- | ---------------------- | 
| Sampling Time (Ts)	        |14 sec |	0.15 × time constant |
| Frequency Bandwidth (ω)	    |0.1452 |	k = 3				 |
| Step Size                     |[-1.5, 1.5] |0.75 × Step Input  |

Results and Discussion
### 1. Data Preprocessing
Outliers detected using 3rd order ARX model.
7 outliers in Z_L and 16 outliers in Z_R were replaced using predicted values.
### 2. Impulse Response Analysis
Time delay determined using MATLAB’s delayest function.
Time delay for Z_L: [1, 2] | Time delay for Z_R: [1, 1]

### 3. Frequency Response Analysis
Frequency response computed using MATLAB’s bode function.
Results show similar magnitude trends but different phase shifts at higher frequencies.

### 4. Model Identification and Validation
The following models were tested:

| Model Type   | MISO Z_L Model Fit (%) | MISO Z_R Model Fit (%) | AIC          
|-------------|----------------------|----------------------|----------------|
| ARX        | 90.99%                | 78.44%                | -12.9          |
| ARMAX      | 91.81%                | 80.59%                | -12.7          |
| OE         | 92.75%                | 78.01%                | -11.7 (Lowest) |
| BJ         | **92.75% (Best)**      | **83.65% (Best)**      | -12.6          |
| Non-Linear | 88.88%                | 80.58%                | -12.9          |
| Subspace   | 82.31%                | 77.17%                | -12.7          |

Best vs. Optimal Models
Best Model: BJ Model (92.75% for Z_L, 83.65% for Z_R)
Optimal Model: OE Model (Lowest AIC: -11.7 for Z_L, -9.55 for Z_R)

![Left tank model comparision ](https://github.com/user-attachments/assets/e9dd7de9-3a98-4c31-b917-b18bef83010d)
![Right tank model comparision](https://github.com/user-attachments/assets/049e2843-ab95-49d1-8aab-5e01852b9a00)


### 5. LSTM Model Implementation
Training Data: 500 points | Validation Data: 215 points

Z_L Fit: 82.12%

Z_R Fit: 60.85% (underperformed due to small dataset)

![LSTM left validation](https://github.com/user-attachments/assets/732a4d0c-29f8-4b1e-8aa3-7358a41b743a)
![LSTM right validation ](https://github.com/user-attachments/assets/4cbb3e60-2ce0-41f5-904c-9509365ad979)

## Conclusion
BJ Model outperformed other models in terms of accuracy.

OE Model is optimal when considering complexity (lowest AIC).

LSTM Model performed poorly due to insufficient training data.
