# How To: High Variance Confounds

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test high_variance_confounds.

## Prerequisites

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.preprocessing`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.masking`
- `nilearn.surface.surface`


## Step-by-Step Guide

### Step 1: 'Test high_variance_confounds.'

```python
'Test high_variance_confounds.'
```

**Verification:**
```python
assert_array_equal(tseries1, tseries2)
```

### Step 2: Assign unknown = _simu_img(...)

```python
img, mask, conf = _simu_img()
```

### Step 3: Assign hv_confounds = high_variance_confounds(...)

```python
hv_confounds = high_variance_confounds(img)
```

### Step 4: Assign masker1 = NiftiMasker.fit(...)

```python
masker1 = NiftiMasker(standardize='zscore_sample', detrend=False, high_variance_confounds=False, mask_img=mask).fit()
```

### Step 5: Assign tseries1 = masker1.transform(...)

```python
tseries1 = masker1.transform(img, confounds=[hv_confounds, conf])
```

### Step 6: Assign masker2 = NiftiMasker.fit(...)

```python
masker2 = NiftiMasker(standardize='zscore_sample', detrend=False, high_variance_confounds=True, mask_img=mask).fit()
```

### Step 7: Assign tseries2 = masker2.transform(...)

```python
tseries2 = masker2.transform(img, confounds=conf)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(tseries1, tseries2)
```


## Complete Example

```python
# Workflow
'Test high_variance_confounds.'
img, mask, conf = _simu_img()
hv_confounds = high_variance_confounds(img)
masker1 = NiftiMasker(standardize='zscore_sample', detrend=False, high_variance_confounds=False, mask_img=mask).fit()
tseries1 = masker1.transform(img, confounds=[hv_confounds, conf])
masker2 = NiftiMasker(standardize='zscore_sample', detrend=False, high_variance_confounds=True, mask_img=mask).fit()
tseries2 = masker2.transform(img, confounds=conf)
assert_array_equal(tseries1, tseries2)
```

## Next Steps


---

*Source: test_masking.py:93 | Complexity: Advanced | Last updated: 2026-05-18*