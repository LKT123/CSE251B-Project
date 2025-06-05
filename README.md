# CSE 251B 2025 Spring Course Project

## 1. Project Description: Trajectory Prediction Challenge
This competition focuses on developing accurate motion forecasting models using the Argoverse 2 Motion Forecasting Dataset. Participants will predict future trajectories of diverse agents (vehicles, pedestrians, cyclists, etc.) in complex, real-world driving scenarios.

We use a modified version of the Argoverse 2 dataset which provides 11-second scenarios with 2D bird's-eye-view data (centroid and heading) sampled at 10Hz. This dataset is designed to challenge models with long-range predictions, diverse agent behaviors, complex social interactions, and rare, critical events.

The goal is to develop models that accurately predict future trajectories, contributing to the advancement of safe and reliable autonomous driving systems. We aim to give you a taste of what is like to do machine learning IRL. Plus, let's be real, who doesn't want to say they taught a computer to see the future?

Also see this link: https://www.kaggle.com/competitions/cse-251-b-2025/overview

## 2. Implementation

Major focuses are on the data augmentation and model architecture. For a given data sample, we have 50 possible agents, and the task is to predict the agent 0's trajectory. Given the data size of 10,000, I augment the data to 80,000 by switching the target I want to predict. (While this has been the largest data size that would be able to fit in my hardware). The augmentation significantly improve the performance.

Another part is the transformer architecture. We use 4 layers with 64 heads of attention. The embedding method is to vectorize the agent's velocities, positions, and so on based on the time scale. This does show a siginificant improvement compared to adding attention mechinisms to the LSTM structure. 

## 3. Improvement

The key chanllenge here is we do not have a good way to interpret the traffic light information. It's viable to keep scale up the model and use more robust hardware (mainly RAM memory for holding the dataset), but encode the traffic light would help a lot. We do try to add the positional encoding to the transformer, but the improvement seems to be rather limited.

A possible way may be to have a seprate model to predict the presense of traffic light nearby as an inductive bias. This may require some feature engineering and data preprocessing to take the data as input and output the situation of the traffic light.
