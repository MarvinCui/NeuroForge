# How To: Resample Scipy

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test resampling against SciPy.

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

### Step 1: 'Test resampling against SciPy.'

```python
'Test resampling against SciPy.'
```

**Verification:**
```python
assert_allclose(x_2, x_2_sp, atol=1e-12, err_msg=err_msg)
```

### Step 2: Assign n_jobs_test = value

```python
n_jobs_test = (1, 'cuda')
```

**Verification:**
```python
assert_allclose(x_p5, x_p5_sp, atol=1e-12, err_msg=err_msg)
```

### Step 3: Assign x = np.arange.astype(...)

```python
x = np.arange(N).astype(float)
```

### Step 4: Assign err_msg = value

```python
err_msg = f'{N}: {window}'
```

### Step 5: Assign x_2_sp = sp_resample(...)

```python
x_2_sp = sp_resample(x, 2 * N, window=window)
```

### Step 6: Assign new_len = int(...)

```python
new_len = int(round(len(x) * (1.0 / 2.0)))
```

### Step 7: Assign x_p5_sp = sp_resample(...)

```python
x_p5_sp = sp_resample(x, new_len, window=window)
```

### Step 8: Assign x_2 = resample(...)

```python
x_2 = resample(x, 2, 1, npad=0, window=window, n_jobs=n_jobs)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(x_2, x_2_sp, atol=1e-12, err_msg=err_msg)
```

### Step 10: Assign x_p5 = resample(...)

```python
x_p5 = resample(x, 1, 2, npad=0, window=window, n_jobs=n_jobs)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(x_p5, x_p5_sp, atol=1e-12, err_msg=err_msg)
```


## Complete Example

```python
# Workflow
'Test resampling against SciPy.'
n_jobs_test = (1, 'cuda')
for window in ('boxcar', 'hann'):
    for N in (100, 101, 102, 103):
        x = np.arange(N).astype(float)
        err_msg = f'{N}: {window}'
        x_2_sp = sp_resample(x, 2 * N, window=window)
        for n_jobs in n_jobs_test:
            x_2 = resample(x, 2, 1, npad=0, window=window, n_jobs=n_jobs)
            assert_allclose(x_2, x_2_sp, atol=1e-12, err_msg=err_msg)
        new_len = int(round(len(x) * (1.0 / 2.0)))
        x_p5_sp = sp_resample(x, new_len, window=window)
        for n_jobs in n_jobs_test:
            x_p5 = resample(x, 1, 2, npad=0, window=window, n_jobs=n_jobs)
            assert_allclose(x_p5, x_p5_sp, atol=1e-12, err_msg=err_msg)
```

## Next Steps


---

*Source: test_filter.py:400 | Complexity: Advanced | Last updated: 2026-05-18*