#machinelearning #sem5 
## Fixed Data Splits
![[Pasted image 20241022215607.png#invert]]
- With “large” datasets (say, >= 1000 examples), it is common to randomly partition the dataset into a training (~80%) and a testing (~20%) portion.
- This split is used for all experimentation by all researchers.
- After estimating accuracy on the test set, we can train the model once more on the entire dataset.
- In many situations in ML, there are both parameters and hyperparameter to optimize. In this case, we need a third data subset for “validation” (hyperparameter optimization):

Alternatively, we can use double cross-validation (though this is computationally expensive).
## Cross Validation
![[Pasted image 20241022215729.png#invert]]
- For “small” datasets, a single test set may not give a reliable accuracy estimate.
- Instead, we can “rotate” which data are used for training vs. testing.
- Cross Validation may need to run several times to give reliable results (e.g. 100 times for 5-fold CV with different random folds).
- Cross Validation Score is averaged over all these runs for all data folds.
- After Cross Validation, the entire dataset can be used to train the model.
### Leave-one-out Cross Validation LOOCV
- De-facto n-fold cross validation, with n number of training samples
- Train the model on n-1 samples and evaluate it on the single data point
- Computing expensive
- Useful especially for small datasets
![[Pasted image 20241022220349.png#invert]]
### Python Example

```python
from sklearn.metrics import accuracy_score

def kFoldCV (n: int, k: int):
  idxsTr = []
  idxsTe = []

  fold_size = n // k
  remainder = n % k
  
  indices = list(range(n))
  
  start = 0
  for i in range(k):
    end = start + fold_size + (1 if i < remainder else 0)  # Add 1 if in remainder folds
    
    test_indices = indices[start:end]
    idxsTe.append(test_indices)
    
    train_indices = indices[:start] + indices[end:]
    idxsTr.append(train_indices)
    
    start = end
    
  return idxsTr, idxsTe

def computeCVAccuracy (k):
  idxsTr, idxsTe = kFoldCV(len(X), k)
  accuracies = []
  
  for train_idx, test_idx in zip(idxsTr, idxsTe):
    # Train the model on the training data
    X_train, y_train = X[train_idx], y[train_idx]
    X_test, y_test = X[test_idx], y[test_idx]
    
    model = LogisticRegression()
    model.fit(X_train, y_train)
    
    # Test the model on the test data
    y_pred = model.predict(X_test)
    accuracy = accuracy_score(y_test, y_pred)
    accuracies.append(accuracy)
  
  # Calculate mean and standard deviation of accuracies
  mean_accuracy = np.mean(accuracies)
  std_accuracy = np.std(accuracies)
  
  return mean_accuracy, std_accuracy

k_values = [5, 10, 15, 20, 25, 30]
results = {}

for k in k_values:
    mean_accuracy, std_accuracy = computeCVAccuracy(k)
    results[k] = (mean_accuracy, std_accuracy)

for k, (mean_acc, std_acc) in results.items():
    print(f"For k={k}, Mean Accuracy: {mean_acc:.4f}, Std Dev: {std_acc:.4f}")
```