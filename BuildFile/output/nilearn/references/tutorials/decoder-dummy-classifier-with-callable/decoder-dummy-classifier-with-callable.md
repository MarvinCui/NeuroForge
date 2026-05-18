# How To: Decoder Dummy Classifier With Callable

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test decoder dummy classifier with callable

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

### Step 1: Assign unknown = binary_classification_data

```python
X, y, mask = binary_classification_data
```

**Verification:**
```python
assert model.scoring == accuracy_scorer
```

### Step 2: Assign accuracy_scorer = get_scorer(...)

```python
accuracy_scorer = get_scorer('accuracy')
```

**Verification:**
```python
assert model.score(X, y) == accuracy_score(y, y_pred)
```

### Step 3: Assign model = Decoder(...)

```python
model = Decoder(estimator='dummy_classifier', mask=mask, scoring=accuracy_scorer, standardize='zscore_sample')
```

### Step 4: Call model.fit()

```python
model.fit(X, y)
```

### Step 5: Assign y_pred = model.predict(...)

```python
y_pred = model.predict(X)
```

**Verification:**
```python
assert model.scoring == accuracy_scorer
```


## Complete Example

```python
# Setup
# Fixtures: binary_classification_data

# Workflow
X, y, mask = binary_classification_data
accuracy_scorer = get_scorer('accuracy')
model = Decoder(estimator='dummy_classifier', mask=mask, scoring=accuracy_scorer, standardize='zscore_sample')
model.fit(X, y)
y_pred = model.predict(X)
assert model.scoring == accuracy_scorer
assert model.score(X, y) == accuracy_score(y, y_pred)
```

## Next Steps


---

*Source: test_decoder.py:802 | Complexity: Intermediate | Last updated: 2026-05-18*