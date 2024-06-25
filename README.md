# my-predictive-modeling-challenge
Repository for predictive modeling challenge 
# Wind Farm Electricity Output Prediction

## Table of Contents
- [Introduction](#introduction)
- [Project Goal](#project-goal)
- [Data Source](#data-source)
- [Setup](#setup)
- [Usage](#usage)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Feature Engineering](#feature-engineering)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Prediction on New Data](#prediction-on-new-data)
- [Results](#results)
- [Conclusion](#conclusion)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Introduction
This project aims to develop a predictive model to forecast the electricity output (CF) of a wind farm based on wind speed data from various locations. The model's performance will be evaluated using the Mean Absolute Error (MAE) metric.

## Project Goal
The primary goal is to build a forecast model that accurately predicts the electricity output (CF) using historical wind speed data.

## Data Source
- **Train Sheet**: Historical data used for training the model.
  - Column B – "CF": Target variable representing the electricity output.
  - Columns C to DJ: Wind speed data from different locations.
- **Predict Sheet**: Data for prediction, containing wind speed features.

## Setup
### Prerequisites
- Python 3.6 or higher
- Jupyter Notebook

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/Maggie-prog/my-cf-electricity-output-prediction-challange.git
   cd my-cf-electricity-output-prediction-challange
