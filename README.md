# Workload Prediction using Centralized Learning and Federated Learning

## Overview:

This project implements workload prediction for cloud and edge computing environments using the Materna workload trace dataset.
The study compares four recurrent neural network architectures:

LSTM,GRU,BiLSTM,BiGRU

under two training paradigms:

-Centralized Learning
-Federated Learning (FedAvg)

The goal is to accurately forecast future CPU utilization while evaluating the trade-off between prediction accuracy and privacy-preserving distributed training.

## Datasets:
-Materna T-13
-Bitbrains
-Microsoft azure

-Materna dataset
 First trace from Materna T-13 workload dataset was used.
 Target variable : CPU usage [%]

## Data preprocessing:

-Missing value handling
-Min-Max normalization
-Sliding window sequence generation

## Parameters and Hyperparameters:

-All models used 40 hidden units in each layer.
-Batch size : 32
-Optimizer : Adam
-Learning Rate : 0.001
-Loss function : MSE/Huber
-Train,test,validation split : 60,20,20
-Epochs : 85 with EarlyStopping
-Early Stopping Patience : 50
-Learning Rate Scheduler : ReduceLROnPlateau

-Federated clients : 5
-Federated rounds : 10
-Local epochs : 6
-Aggregation Algorithm : FedAvg(Federated Averaging)

## Models Evaluated:

-LSTM
 Long Short-Term Memory network for learning temporal dependencies.

-GRU
 Gated Recurrent Unit with fewer parameters and faster training.

-BiLSTM
 Bidirectional LSTM capable of learning dependencies from both directions.

-BiGRU
 Bidirectional GRU capable of learning dependencies from both directions with lower computational complexity.

## Centralized Learning:

In the centralized approach, workload traces from all selected clients are aggregated and used to train a single global model.

Advantages:

-Higher prediction accuracy
-Complete visibility of training data

Limitations:

-Requires data sharing
-Privacy concerns
-Federated Learning

## Federated Learning: 

Federated Learning trains models locally on client devices and exchanges only model parameters.
FedAvg aggregation is used to construct the global model.
Experiment is done using 5 clients and got better prediction with 10 Federated rounds.

Advantages:

-Preserves data privacy
-Reduces raw data transfer
-Suitable for distributed edge environments
-Evaluation Metrics

## The following metrics are reported:

MAE,MSE,RMSE,RMSLE

Lower values indicate better prediction performance.

## Key Findings:

- Bidirectional architectures (BiLSTM and BiGRU) consistently outperformed conventional LSTM and GRU models.
- Increasing the window size improved forecasting performance up to a certain point, with Window Size 16 
  providing a strong balance between accuracy and computational cost.
- BiLSTM and BiGRU achieved nearly identical performance across most experiments, indicating that both 
  architectures effectively capture workload dynamics.
- Federated Learning produced results close to centralized learning while preserving data privacy and reducing 
  the need for raw data sharing.
- The study demonstrates that privacy-preserving workload prediction can be achieved without a substantial 
  loss in forecasting accuracy.

## RMSE for (Materna Dataset, Window Size = 16):

Model	 RMSE
BiLSTM	 0.128
BiGRU	 0.125

The small difference indicates that both bidirectional architectures are highly effective and good for workload prediction.

## Future Work:

  -Transformer-based forecasting models
  -Attention mechanisms
  -Multivariate prediction
  -Real-time workload prediction for auto-scaling systems    
