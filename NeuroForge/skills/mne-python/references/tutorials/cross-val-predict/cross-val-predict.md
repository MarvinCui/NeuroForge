# How To: Cross Val Predict

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test cross_val_predict with predict_proba.

## Prerequisites

**Required Modules:**
- `platform`
- `inspect`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.base`
- `sklearn.discriminant_analysis`
- `sklearn.ensemble`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.multiclass`
- `sklearn.pipeline`
- `sklearn.svm`
- `sklearn.utils.estimator_checks`
- `mne.decoding.search_light`
- `mne.decoding.transformer`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test cross_val_predict with predict_proba.'

```python
'Test cross_val_predict with predict_proba.'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

### Step 3: Assign X = rng.randn(...)

```python
X = rng.randn(10, 1, 3)
```

### Step 4: Assign y = rng.randint(...)

```python
y = rng.randint(0, 2, 10)
```

### Step 5: Assign estimator = SlidingEstimator(...)

```python
estimator = SlidingEstimator(LinearRegression())
```

### Step 6: Call cross_val_predict()

```python
cross_val_predict(estimator, X, y, cv=2)
```

### Step 7: Assign estimator = SlidingEstimator(...)

```python
estimator = SlidingEstimator(LinearDiscriminantAnalysis())
```

### Step 8: Call cross_val_predict()

```python
cross_val_predict(estimator, X, y, method='predict_proba', cv=2)
```

### Step 9: """Moch class that does not have classes_ attribute."""

```python
"""Moch class that does not have classes_ attribute."""
```

### Step 10: Assign estimator = SlidingEstimator(...)

```python
estimator = SlidingEstimator(Classifier())
```

### Step 11: Call cross_val_predict()

```python
cross_val_predict(estimator, X, y, method='predict_proba', cv=2)
```

### Step 12: Assign self.base_estimator = LinearDiscriminantAnalysis(...)

```python
self.base_estimator = LinearDiscriminantAnalysis()
```

### Step 13: Assign self.estimator_ = clone.fit(...)

```python
self.estimator_ = clone(self.base_estimator).fit(X, y)
```


## Complete Example

```python
# Workflow
'Test cross_val_predict with predict_proba.'
rng = np.random.RandomState(42)
X = rng.randn(10, 1, 3)
y = rng.randint(0, 2, 10)
estimator = SlidingEstimator(LinearRegression())
cross_val_predict(estimator, X, y, cv=2)

class Classifier(BaseEstimator):
    """Moch class that does not have classes_ attribute."""

    def __init__(self):
        self.base_estimator = LinearDiscriminantAnalysis()

    def fit(self, X, y):
        self.estimator_ = clone(self.base_estimator).fit(X, y)
        return self

    def predict_proba(self, X):
        return self.estimator_.predict_proba(X)
with pytest.raises(AttributeError, match='classes_ attribute'):
    estimator = SlidingEstimator(Classifier())
    cross_val_predict(estimator, X, y, method='predict_proba', cv=2)
estimator = SlidingEstimator(LinearDiscriminantAnalysis())
cross_val_predict(estimator, X, y, method='predict_proba', cv=2)
```

## Next Steps


---

*Source: test_search_light.py:319 | Complexity: Advanced | Last updated: 2026-05-18*