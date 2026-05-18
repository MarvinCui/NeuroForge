# How To: Nilearn Standardize

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test confounds removal with logical parameters for processing signal.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `scipy.stats`
- `sklearn.preprocessing`
- `nilearn._utils.data_gen`
- `nilearn._utils.fmriprep_confounds`
- `nilearn.conftest`
- `nilearn.interfaces.bids`
- `nilearn.interfaces.fmriprep`
- `nilearn.interfaces.fmriprep.load_confounds`
- `nilearn.interfaces.fmriprep.tests._testing`
- `nilearn.maskers`
- `nilearn.tests.test_signal`
- `inspect`

**Setup Required:**
```python
# Fixtures: tmp_path, standardize_signal, standardize_confounds, detrend
```

## Step-by-Step Guide

### Step 1: 'Test confounds removal with logical parameters for processing signal.'

```python
'Test confounds removal with logical parameters for processing signal.'
```

**Verification:**
```python
assert np.absolute(np.mean(corr)) < 0.2
```

### Step 2: Assign unknown = _simu_img(...)

```python
img, mask_conf, mask_rand, confounds, mask = _simu_img(tmp_path, trend=True, demean=False)
```

**Verification:**
```python
assert corr.mean() > 0.8
```

### Step 3: Assign unknown = _denoise(...)

```python
tseries_raw, tseries_clean = _denoise(img, mask_conf, confounds, mask, standardize_signal=standardize_signal, standardize_confounds=standardize_confounds, detrend=detrend)
```

### Step 4: Assign corr = _corr_tseries(...)

```python
corr = _corr_tseries(tseries_raw, tseries_clean)
```

**Verification:**
```python
assert np.absolute(np.mean(corr)) < 0.2
```

### Step 5: Assign unknown = _denoise(...)

```python
tseries_raw, tseries_clean = _denoise(img, mask_rand, confounds, mask, standardize_signal=standardize_signal, standardize_confounds=standardize_confounds, detrend=detrend)
```

### Step 6: Assign corr = _corr_tseries(...)

```python
corr = _corr_tseries(tseries_raw, tseries_clean)
```

**Verification:**
```python
assert corr.mean() > 0.8
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, standardize_signal, standardize_confounds, detrend

# Workflow
'Test confounds removal with logical parameters for processing signal.'
img, mask_conf, mask_rand, confounds, mask = _simu_img(tmp_path, trend=True, demean=False)
tseries_raw, tseries_clean = _denoise(img, mask_conf, confounds, mask, standardize_signal=standardize_signal, standardize_confounds=standardize_confounds, detrend=detrend)
corr = _corr_tseries(tseries_raw, tseries_clean)
assert np.absolute(np.mean(corr)) < 0.2
tseries_raw, tseries_clean = _denoise(img, mask_rand, confounds, mask, standardize_signal=standardize_signal, standardize_confounds=standardize_confounds, detrend=detrend)
corr = _corr_tseries(tseries_raw, tseries_clean)
assert corr.mean() > 0.8
```

## Next Steps


---

*Source: test_load_confounds.py:257 | Complexity: Intermediate | Last updated: 2026-05-18*