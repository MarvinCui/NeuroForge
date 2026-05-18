# How To: Decoder Dummy Classifier

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test decoder dummy classifier

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: binary_classification_data
```

## Step-by-Step Guide

### Step 1: Assign n_samples = N_SAMPLES

```python
n_samples = N_SAMPLES
```

**Verification:**
```python
assert np.sum(y_pred == 1.0) / n_samples - proportion < 0.05
```

### Step 2: Assign unknown = binary_classification_data

```python
X, y, mask = binary_classification_data
```

### Step 3: Assign proportion = 0.8

```python
proportion = 0.8
```

### Step 4: Assign y = np.zeros(...)

```python
y = np.zeros(n_samples)
```

### Step 5: Assign unknown = 1.0

```python
y[:int(proportion * n_samples)] = 1.0
```

### Step 6: Assign model = Decoder(...)

```python
model = Decoder(estimator='dummy_classifier', mask=mask, standardize='zscore_sample')
```

### Step 7: Call model.fit()

```python
model.fit(X, y)
```

### Step 8: Assign y_pred = model.predict(...)

```python
y_pred = model.predict(X)
```

**Verification:**
```python
assert np.sum(y_pred == 1.0) / n_samples - proportion < 0.05
```


## Complete Example

```python
# Setup
# Fixtures: binary_classification_data

# Workflow
n_samples = N_SAMPLES
X, y, mask = binary_classification_data
proportion = 0.8
y = np.zeros(n_samples)
y[:int(proportion * n_samples)] = 1.0
model = Decoder(estimator='dummy_classifier', mask=mask, standardize='zscore_sample')
model.fit(X, y)
y_pred = model.predict(X)
assert np.sum(y_pred == 1.0) / n_samples - proportion < 0.05
```

## Next Steps


---

*Source: test_decoder.py:782 | Complexity: Advanced | Last updated: 2026-05-18*