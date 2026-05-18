# How To: Transform Confounds

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test transform with confounds give different results.

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

### Step 1: 'Test transform with confounds give different results.'

```python
'Test transform with confounds give different results.'
```

**Verification:**
```python
assert_raises(AssertionError, assert_array_equal, signals, signals_confounds)
```

### Step 2: Assign est = estimator(...)

```python
est = estimator(n_components=3, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
```

### Step 3: Call est.fit()

```python
est.fit(canica_data)
```

### Step 4: Assign signals = est.transform(...)

```python
signals = est.transform(canica_data)
```

### Step 5: Assign confounds = value

```python
confounds = [np.arange(n_samples * 2).reshape(n_samples, 2)] * len(canica_data)
```

### Step 6: Assign signals_confounds = est.transform(...)

```python
signals_confounds = est.transform(canica_data, confounds=confounds)
```

### Step 7: Call assert_raises()

```python
assert_raises(AssertionError, assert_array_equal, signals, signals_confounds)
```

### Step 8: Call pytest.skip()

```python
pytest.skip('dummy data for surface give empty signals with DictLearning')
```

### Step 9: Assign n_samples = value

```python
n_samples = canica_data[0].shape[1]
```

### Step 10: Assign n_samples = value

```python
n_samples = canica_data[0].shape[3]
```


## Complete Example

```python
# Setup
# Fixtures: data_type, canica_data, estimator

# Workflow
'Test transform with confounds give different results.'
est = estimator(n_components=3, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
if data_type == 'surface' and isinstance(est, DictLearning):
    pytest.skip('dummy data for surface give empty signals with DictLearning')
est.fit(canica_data)
signals = est.transform(canica_data)
if data_type == 'surface':
    n_samples = canica_data[0].shape[1]
else:
    n_samples = canica_data[0].shape[3]
confounds = [np.arange(n_samples * 2).reshape(n_samples, 2)] * len(canica_data)
signals_confounds = est.transform(canica_data, confounds=confounds)
assert_raises(AssertionError, assert_array_equal, signals, signals_confounds)
```

## Next Steps


---

*Source: test_decomposition_estimators.py:208 | Complexity: Advanced | Last updated: 2026-05-18*