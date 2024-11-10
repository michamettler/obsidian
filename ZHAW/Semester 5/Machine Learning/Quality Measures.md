#machinelearning #sem5 

https://github.com/michamettler/zhaw-mldm/blob/main/L05/L05_Supervised_Learning_LAB_ASSIGNMENT.ipynb
## Accuracy
For classification tasks, probably the most common evaluation metric is the **proportion-correct accuracy**, often abbreviated simply as **accuracy**: it is the proportion of the examples that were correctly classified.
![[Pasted image 20241022214729.png]]
## Precision and Recall
Precision and Recall are performance metrics for binary classification problems.
![[Pasted image 20241022214954.png#invert]]
### Precision

$$\text{precision} = \frac{|\text{PredictedPositive} \cap \text{ActualPositive}|}{|\text{PredictedPositive}|}$$
### Recall
What proportion of the actually positive examples did the model predict as positive?
$$\text{recall} = \frac{|\text{PredictedPositive} \cap \text{ActualPositive}|}{|\text{ActualPositive}|}
$$
### F1
For a fixed threshold, we can express both the precision and recall in a single number using an F1-Score:
$$\text{Definition of F1-Score:} \quad F_1 = 2 * \frac{\text{precision} * \text{recall}}{\text{precision} + \text{recall}}
$$
$$
\text{Definition of general } F_\beta\text{-Score:} \quad F_\beta = (1 + \beta^2) * \frac{\text{precision} * \text{recall}}{(\beta^2 * \text{precision}) + \text{recall}}
$$
## Python Example

```python
import seaborn as sns
from sklearn.metrics import confusion_matrix

confusion_matrix_test = sklearn_confusion_matrix = confusion_matrix(y_test, y_test_pred)
print(confusion_matrix_test)

sns.heatmap(confusion_matrix_test, annot=True)

def precision(class_of_interest, confusion_matrix_test):
  return confusion_matrix_test[class_of_interest][class_of_interest] / (confusion_matrix_test[class_of_interest][class_of_interest] + confusion_matrix_test[1-class_of_interest][class_of_interest])

def recall(class_of_interest, confusion_matrix_test):
  return confusion_matrix_test[class_of_interest][class_of_interest] / (confusion_matrix_test[class_of_interest][class_of_interest] + confusion_matrix_test[class_of_interest][1-class_of_interest])

def f1_score(precision_value, recall_value):
  return 2 * precision_value * recall_value / (precision_value + recall_value)

# For Class 0
precision_value = precision(0, confusion_matrix_test)
recall_value = recall(0, confusion_matrix_test)
f1_score_test = f1_score(precision_value, recall_value)

print(f"Precision: {precision_value}")
print(f"Recall: {recall_value}")
print(f"F1-Score: {f1_score_test}")
```
![[Pasted image 20241022215132.png#invert]]
## Find Best Threshold

```python
def findBestThreshold (fpCost, fnCost):
  thresholds = np.arange(0.1, 1.0, 0.1)
  y_probs = log_reg.predict_proba(X_test)[:, 1] 
  
  best_threshold = 0
  best_score = float('inf')
  
  for threshold in thresholds:
    y_pred = (y_probs >= threshold).astype(int)
    
    confusion_matrix_test = confusion_matrix(y_test, y_pred)
    fp = confusion_matrix_test[0][1]
    fn = confusion_matrix_test[1][0]
    
    score = fp * fpCost + fn * fnCost
    
    if score < best_score:
      best_score = score
      best_threshold = threshold
      
  return best_threshold

fpCost = 500
fnCost = 500
best_threshold = findBestThreshold(fpCost, fnCost)
print(f"Best Threshold: {best_threshold}")
```