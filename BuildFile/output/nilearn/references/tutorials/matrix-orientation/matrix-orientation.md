# How To: Matrix Orientation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if processing is performed along the correct axis.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.maskers.nifti_masker`


## Step-by-Step Guide

### Step 1: 'Test if processing is performed along the correct axis.'

```python
'Test if processing is performed along the correct axis.'
```

**Verification:**
```python
assert timeseries.shape[0] == fmri.shape[3]
```

### Step 2: Assign unknown = data_gen.generate_fake_fmri(...)

```python
fmri, mask = data_gen.generate_fake_fmri(shape=(40, 41, 42), kind='step')
```

**Verification:**
```python
assert timeseries.shape[1] == get_data(mask).sum()
```

### Step 3: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask_img=mask, standardize='zscore_sample', detrend=True)
```

**Verification:**
```python
assert std.shape[0] == timeseries.shape[1]
```

### Step 4: Assign timeseries = masker.fit_transform(...)

```python
timeseries = masker.fit_transform(fmri)
```

**Verification:**
```python
assert not np.any(std < 0.1)
```

### Step 5: Assign std = timeseries.std(...)

```python
std = timeseries.std(axis=0)
```

**Verification:**
```python
assert std.shape[0] == timeseries.shape[1]
```

### Step 6: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask_img=mask, standardize=None)
```

### Step 7: Call masker.fit()

```python
masker.fit()
```

### Step 8: Assign timeseries = masker.transform(...)

```python
timeseries = masker.transform(fmri)
```

### Step 9: Assign recovered = masker.inverse_transform(...)

```python
recovered = masker.inverse_transform(timeseries)
```

### Step 10: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(get_data(recovered), get_data(fmri))
```


## Complete Example

```python
# Workflow
'Test if processing is performed along the correct axis.'
fmri, mask = data_gen.generate_fake_fmri(shape=(40, 41, 42), kind='step')
masker = NiftiMasker(mask_img=mask, standardize='zscore_sample', detrend=True)
timeseries = masker.fit_transform(fmri)
assert timeseries.shape[0] == fmri.shape[3]
assert timeseries.shape[1] == get_data(mask).sum()
std = timeseries.std(axis=0)
assert std.shape[0] == timeseries.shape[1]
assert not np.any(std < 0.1)
masker = NiftiMasker(mask_img=mask, standardize=None)
masker.fit()
timeseries = masker.transform(fmri)
recovered = masker.inverse_transform(timeseries)
np.testing.assert_array_almost_equal(get_data(recovered), get_data(fmri))
```

## Next Steps


---

*Source: test_nifti_masker.py:179 | Complexity: Advanced | Last updated: 2026-05-18*