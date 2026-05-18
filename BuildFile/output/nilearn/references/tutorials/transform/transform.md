# How To: Transform

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test transform and inverse transform.

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
# Fixtures: data_type, canica_data, estimator
```

## Step-by-Step Guide

### Step 1: 'Test transform and inverse transform.'

```python
'Test transform and inverse transform.'
```

**Verification:**
```python
assert isinstance(signals, list)
```

### Step 2: Assign est = estimator(...)

```python
est = estimator(n_components=3, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
```

**Verification:**
```python
assert isinstance(x, np.ndarray)
```

### Step 3: Call est.fit()

```python
est.fit(canica_data)
```

**Verification:**
```python
assert_array_equal(signals, signals_2)
```

### Step 4: Assign signals = est.transform(...)

```python
signals = est.transform(canica_data)
```

**Verification:**
```python
assert isinstance(signals, list)
```

### Step 5: Assign est = clone(...)

```python
est = clone(est)
```

### Step 6: Assign signals_2 = est.fit_transform(...)

```python
signals_2 = est.fit_transform(canica_data)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(signals, signals_2)
```

### Step 8: Call est.inverse_transform()

```python
est.inverse_transform(signals)
```

**Verification:**
```python
assert isinstance(x, np.ndarray)
```


## Complete Example

```python
# Setup
# Fixtures: data_type, canica_data, estimator

# Workflow
'Test transform and inverse transform.'
est = estimator(n_components=3, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
est.fit(canica_data)
signals = est.transform(canica_data)
assert isinstance(signals, list)
for x in signals:
    assert isinstance(x, np.ndarray)
est = clone(est)
signals_2 = est.fit_transform(canica_data)
assert_array_equal(signals, signals_2)
est.inverse_transform(signals)
```

## Next Steps


---

*Source: test_decomposition_estimators.py:174 | Complexity: Advanced | Last updated: 2026-05-18*