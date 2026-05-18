# How To: Single Subject Score

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check content of scores after fitting.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.decomposition`
- `nilearn.decomposition._multi_pca`
- `nilearn.decomposition.tests.conftest`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: canica_data_single_img, data_type, estimator
```

## Step-by-Step Guide

### Step 1: 'Check content of scores after fitting.'

```python
'Check content of scores after fitting.'
```

**Verification:**
```python
assert n_components < N_SAMPLES
```

### Step 2: Assign n_components = 3

```python
n_components = 3
```

**Verification:**
```python
assert isinstance(scores, float)
```

### Step 3: Assign est = estimator(...)

```python
est = estimator(n_components=n_components, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
```

**Verification:**
```python
assert 0 <= scores <= 1
```

### Step 4: Call est.fit()

```python
est.fit(canica_data_single_img)
```

**Verification:**
```python
assert scores.shape, (n_components,)
```

### Step 5: Call check_decomposition_estimator()

```python
check_decomposition_estimator(est, data_type)
```

**Verification:**
```python
assert np.all(scores <= 1)
```

### Step 6: Assign scores = est.score(...)

```python
scores = est.score(canica_data_single_img, per_component=False)
```

**Verification:**
```python
assert np.all(scores >= 0)
```

### Step 7: Assign scores = est.score(...)

```python
scores = est.score(canica_data_single_img, per_component=True)
```

**Verification:**
```python
assert scores.shape, (n_components,)
```


## Complete Example

```python
# Setup
# Fixtures: canica_data_single_img, data_type, estimator

# Workflow
'Check content of scores after fitting.'
n_components = 3
assert n_components < N_SAMPLES
est = estimator(n_components=n_components, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
est.fit(canica_data_single_img)
check_decomposition_estimator(est, data_type)
scores = est.score(canica_data_single_img, per_component=False)
assert isinstance(scores, float)
assert 0 <= scores <= 1
scores = est.score(canica_data_single_img, per_component=True)
assert scores.shape, (n_components,)
assert np.all(scores <= 1)
assert np.all(scores >= 0)
```

## Next Steps


---

*Source: test_decomposition_estimators.py:381 | Complexity: Intermediate | Last updated: 2026-05-18*