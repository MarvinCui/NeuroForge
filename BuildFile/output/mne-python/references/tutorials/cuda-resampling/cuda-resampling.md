# How To: Cuda Resampling

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test CUDA resampling.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy.signal`
- `scipy.signal`
- `mne`
- `mne._fiff.pick`
- `mne.filter`
- `mne.io`
- `mne.utils`
- `mne.cuda`


## Step-by-Step Guide

### Step 1: 'Test CUDA resampling.'

```python
'Test CUDA resampling.'
```

**Verification:**
```python
assert_allclose(a1, a2, rtol=1e-07, atol=1e-14)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_array_almost_equal(a1, a2, 14)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(a1, a2, 14)
```

**Verification:**
```python
assert_array_equal(resample(np.zeros(2), 2, 1, n_jobs='cuda'), np.zeros(4))
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(resample(np.zeros(2), 2, 1, n_jobs='cuda'), np.zeros(4))
```

### Step 5: Assign a = rng.randn(...)

```python
a = rng.randn(2, N)
```

### Step 6: Assign a1 = resample(...)

```python
a1 = resample(a, fro, to, n_jobs=None, npad='auto', window=window)
```

### Step 7: Assign a2 = resample(...)

```python
a2 = resample(a, fro, to, n_jobs='cuda', npad='auto', window=window)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(a1, a2, rtol=1e-07, atol=1e-14)
```


## Complete Example

```python
# Workflow
'Test CUDA resampling.'
rng = np.random.RandomState(0)
for window in ('boxcar', 'triang'):
    for N in (997, 1000):
        a = rng.randn(2, N)
        for fro, to in ((1, 2), (2, 1), (1, 3), (3, 1)):
            a1 = resample(a, fro, to, n_jobs=None, npad='auto', window=window)
            a2 = resample(a, fro, to, n_jobs='cuda', npad='auto', window=window)
            assert_allclose(a1, a2, rtol=1e-07, atol=1e-14)
assert_array_almost_equal(a1, a2, 14)
assert_array_equal(resample(np.zeros(2), 2, 1, n_jobs='cuda'), np.zeros(4))
```

## Next Steps


---

*Source: test_filter.py:846 | Complexity: Advanced | Last updated: 2026-05-18*