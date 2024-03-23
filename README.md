# IOTML

In view of object detection tasks the deployment of machine learning models on raspberry pi requires a fine tuning between model’s accuracy and its complexity to achieve best results.
In this project we examined various machine learning models and deep learning architectures for thermal comfort prediction, While considering the above mentioned aspects with smooth functioning of edge device; Raspberry pi being the main objective.

**Database**

ASHRAE 55 defines thermal comfort as “that condition of mind that expresses satisfaction with the thermal environment”, and is used primarily in the United States but is well known around the world as the standard for designing, commissioning, and testing indoor spaces and systems.

**Data pre-preparation**

We chose to pick out the important features from the set of features described in the table during data cleaning by eliminating all the columns with greater than 20 percent of NULL values to reduce the overhead on the algorithm along with elimination of unimportnat features in the database.

| features  | percentage of missing values(%) |
| ------------- | ------------- |
| Cooling strategy building level  | 0.03 |
| Climate  | 0  |
| Country  | 0  |
| Clothing  | 7  |
| Air temperature (C)  | 2.2  |
| Relative humidity  | 9.3  |
| Air velocity (m/s)  | 13.6  |
| Metabolic rate  | 15  |
| Age  | 68  |
| Sex   | 42.8  |
| Climate  | 0  |

we picked out the subset of features T{Cooling startegy building level, Climate, Season, Country,Thermal sensation, Clothing, Air temperature (C),Relative humidity,Air velocity (m/s), Met} among the above.

**Data cleaning**

The data source was an open-source research databases in advancing the art and science of HVAC,the ASHRAE Global Thermal Comfort Database II project. But the raw data needed data cleaning and feature selction before proceeding further.
we used KNN imputer to fill in the null values in various columns[Example PDF](PDFs/example.pdf) 
The performance of the kNN imputer was proven surpassing the traditional methods such as filling missing values with zeros, row average, or previous instance owing to its effective utilization of correlation structure of the data within a dataset. The kNN imputer is also robust against increasing percentage of missing values while maintaining a rapid computation.

**Dimensionality Reduction**

we used the Dimensionality reduction technique 'Neighborhood component analysis'.
Neighborhood component analysis (NCA) is a non-parametric method for selecting features with the goal of maximizing prediction accuracy of regression and classification algorithms.
After applying PCA,The weights all features are plotted across a graph and we considered all the features whose weight is greater than 5\% of the highest weighted feature. We experimented on various percentages(5\%,15\%,20\%) and found that 5\% is the best proportion to consider as cutoff.

**Model development**

The models used are random forest regression,Artificial neural network and the model optimization technique used is pruning on the thermal comfort data based models.

_Random Forest Regression_

It is known that random forest algorithm is the best performer among all other tree based algorithms such as gradient boosting trees and extra tree algorithms.Thus we have chosen random forest as the representation of tree based models.

**Model Evaluation**

_Mean Squared Error_
While the Mean squared error is the most common loss function in machine learning.It is a perfect loss function to make sure that our model's predictions do not have a lot of outliers.
\end{gather}

_Mean Absolute Error_
MAE loss function takes absolute difference between ground truth and predicted values.Since the absolute values is calculates all the errors are weighted similarly giving a overall outlay of the performance of model.

**optimizing techniques**

The neural networks or Tree based models are in general very complex in nature.While running those models on a memory constraint edge device, We have to make sure they are made as less complex as possible.So we use the optimizing techniques to improve the complexity of the models.The most common optimisation technique used before deploying the deep learning architectures is model pruning. 
_pruning_
A Tree based model can be optimised in terms of accuracy or loss by which the less important nodes in the model are pruned and an efficient model is presented with a very less accuracy loss.But the complexity is very much improved.
While the neural networks can be made efficient in terms of complexity using single shot pruning.A more recent method has been proposed called _iterative pruning_ for feed forward networks which is found to be much better compared to single shot pruning.We will use the iterative pruning method on our neural network while making sure the accuracy loss is as low as possible.

**Results**
Below are the results of applying above mentioned tehniques
Model&Train MSE loss&Test MSE loss\\
 \hline
 Baseline&0.79&0.77\\
 Pruned&0.08&0.07\\
 model conversion&0.04&0.04\\
 quantization&0.08&0.06\\

| Model  | Train MSE | Test MSE |
| ------------- | ------------- | ------------- |
| Baseline  | 0.79 | 0.77 |
| pruned | 0.08 | 0.07 |
| model conversion  | 0.04 | 0.04
| Model quantization | 0.08 | 0.06 |
 




























