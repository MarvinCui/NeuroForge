# How To: With Confounds

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test of estimator with confounds.

Output should be different with and without confounds.

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
# Fixtures: data_type, decomposition_images, decomposition_mask_img, estimator
```

## Step-by-Step Guide

### Step 1: 'Test of estimator with confounds.\n\n    Output should be different with and without confounds.\n    '

```python
'Test of estimator with confounds.\n\n    Output should be different with and without confounds.\n    '
```

**Verification:**
```python
assert_raises(AssertionError, assert_array_equal, components, components_clean)
```

### Step 2: Assign confounds = value

```python
confounds = [np.arange(N_SAMPLES * 2).reshape(N_SAMPLES, 2)] * N_SUBJECTS
```

### Step 3: Assign est = estimator(...)

```python
est = estimator(n_components=3, random_state=RANDOM_STATE, mask=decomposition_mask_img, smoothing_fwhm=None, standardize='zscore_sample')
```

### Step 4: Call est.fit()

```python
est.fit(decomposition_images)
```

### Step 5: Call check_decomposition_estimator()

```python
check_decomposition_estimator(est, data_type)
```

### Step 6: Assign components = value

```python
components = est.components_
```

### Step 7: Assign est = estimator(...)

```python
est = estimator(n_components=3, random_state=RANDOM_STATE, mask=decomposition_mask_img)
```

### Step 8: Call est.fit()

```python
est.fit(decomposition_images, confounds=confounds)
```

### Step 9: Assign components_clean = value

```python
components_clean = est.components_
```

### Step 10: Call assert_raises()

```python
assert_raises(AssertionError, assert_array_equal, components, components_clean)
```


## Complete Example

```python
# Setup
# Fixtures: data_type, decomposition_images, decomposition_mask_img, estimator

# Workflow
'Test of estimator with confounds.\n\n    Output should be different with and without confounds.\n    '
confounds = [np.arange(N_SAMPLES * 2).reshape(N_SAMPLES, 2)] * N_SUBJECTS
est = estimator(n_components=3, random_state=RANDOM_STATE, mask=decomposition_mask_img, smoothing_fwhm=None, standardize='zscore_sample')
est.fit(decomposition_images)
check_decomposition_estimator(est, data_type)
components = est.components_
est = estimator(n_components=3, random_state=RANDOM_STATE, mask=decomposition_mask_img)
est.fit(decomposition_images, confounds=confounds)
components_clean = est.components_
assert_raises(AssertionError, assert_array_equal, components, components_clean)
```

## Next Steps


---

*Source: test_decomposition_estimators.py:343 | Complexity: Advanced | Last updated: 2026-05-18*