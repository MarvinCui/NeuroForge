# How To: Decoder Dummy Classifier Strategy Prior

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test decoder dummy classifier strategy prior

## Prerequisites

**Required Modules:**
- `collections`
- `numbers`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn`
- `sklearn`
- `sklearn.datasets`
- `sklearn.dummy`
- `sklearn.ensemble`
- `sklearn.exceptions`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.preprocessing`
- `sklearn.svm`
- `sklearn.utils._testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.decoding`
- `nilearn.decoding._utils`
- `nilearn.decoding.decoder`
- `nilearn.decoding.tests.test_same_api`
- `nilearn.maskers`


## Step-by-Step Guide

### Step 1: Assign unknown = _make_binary_classification_test_data(...)

```python
X, y, mask = _make_binary_classification_test_data(n_samples=300)
```

**Verification:**
```python
assert np.all(y_pred) == 1.0
```

### Step 2: Assign param = value

```python
param = {'strategy': 'prior'}
```

**Verification:**
```python
assert roc_auc_score(y, y_pred) == 0.5
```

### Step 3: Assign dummy_classifier = DummyClassifier(...)

```python
dummy_classifier = DummyClassifier(random_state=0)
```

### Step 4: Call dummy_classifier.set_params()

```python
dummy_classifier.set_params(**param)
```

### Step 5: Assign model = Decoder(...)

```python
model = Decoder(estimator=dummy_classifier, mask=mask, standardize='zscore_sample')
```

### Step 6: Call model.fit()

```python
model.fit(X, y)
```

### Step 7: Assign y_pred = model.predict(...)

```python
y_pred = model.predict(X)
```

**Verification:**
```python
assert np.all(y_pred) == 1.0
```


## Complete Example

```python
# Workflow
X, y, mask = _make_binary_classification_test_data(n_samples=300)
param = {'strategy': 'prior'}
dummy_classifier = DummyClassifier(random_state=0)
dummy_classifier.set_params(**param)
model = Decoder(estimator=dummy_classifier, mask=mask, standardize='zscore_sample')
model.fit(X, y)
y_pred = model.predict(X)
assert np.all(y_pred) == 1.0
assert roc_auc_score(y, y_pred) == 0.5
```

## Next Steps


---

*Source: test_decoder.py:819 | Complexity: Intermediate | Last updated: 2026-05-18*