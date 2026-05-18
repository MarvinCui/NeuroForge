# How To: Cuda Fir

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test CUDA-based filtering.

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

### Step 1: 'Test CUDA-based filtering.'

```python
'Test CUDA-based filtering.'
```

**Verification:**
```python
assert_array_almost_equal(bp, bp_c, 12)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_array_almost_equal(bs, bs_c, 12)
```

### Step 3: Assign sfreq = 500

```python
sfreq = 500
```

**Verification:**
```python
assert_array_almost_equal(lp, lp_c, 12)
```

### Step 4: Assign sig_len_secs = 20

```python
sig_len_secs = 20
```

**Verification:**
```python
assert_array_almost_equal(hp, hp_c, 12)
```

### Step 5: Assign a = rng.randn(...)

```python
a = rng.randn(sig_len_secs * sfreq)
```

**Verification:**
```python
assert sum(['Using CUDA for FFT FIR filtering' in o for o in out]) == tot
```

### Step 6: Assign kwargs = dict(...)

```python
kwargs = dict(fir_design='firwin')
```

### Step 7: Assign out = value

```python
out = log_file.getvalue().split('\n')[:-1]
```

### Step 8: Assign tot = value

```python
tot = 12 if _cuda_capable else 0
```

**Verification:**
```python
assert sum(['Using CUDA for FFT FIR filtering' in o for o in out]) == tot
```

### Step 9: Call pytest.skip()

```python
pytest.skip('CUDA not enabled')
```

### Step 10: Assign args = value

```python
args = [a, sfreq, 4, 8, None, fl, 1.0, 1.0]
```

### Step 11: Assign bp = filter_data(...)

```python
bp = filter_data(*args, **kwargs)
```

### Step 12: Assign bp_c = filter_data(...)

```python
bp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(bp, bp_c, 12)
```

### Step 14: Assign args = value

```python
args = [a, sfreq, 8 + 1.0, 4 - 1.0, None, fl, 1.0, 1.0]
```

### Step 15: Assign bs = filter_data(...)

```python
bs = filter_data(*args, **kwargs)
```

### Step 16: Assign bs_c = filter_data(...)

```python
bs_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(bs, bs_c, 12)
```

### Step 18: Assign args = value

```python
args = [a, sfreq, None, 8, None, fl, 1.0]
```

### Step 19: Assign lp = filter_data(...)

```python
lp = filter_data(*args, **kwargs)
```

### Step 20: Assign lp_c = filter_data(...)

```python
lp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
```

### Step 21: Call assert_array_almost_equal()

```python
assert_array_almost_equal(lp, lp_c, 12)
```

### Step 22: Assign args = value

```python
args = [lp, sfreq, 4, None, None, fl, 1.0]
```

### Step 23: Assign hp = filter_data(...)

```python
hp = filter_data(*args, **kwargs)
```

### Step 24: Assign hp_c = filter_data(...)

```python
hp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
```

### Step 25: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hp, hp_c, 12)
```


## Complete Example

```python
# Workflow
'Test CUDA-based filtering.'
rng = np.random.RandomState(0)
sfreq = 500
sig_len_secs = 20
a = rng.randn(sig_len_secs * sfreq)
kwargs = dict(fir_design='firwin')
with catch_logging() as log_file:
    for fl in ['auto', '10s', 2048]:
        args = [a, sfreq, 4, 8, None, fl, 1.0, 1.0]
        bp = filter_data(*args, **kwargs)
        bp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(bp, bp_c, 12)
        args = [a, sfreq, 8 + 1.0, 4 - 1.0, None, fl, 1.0, 1.0]
        bs = filter_data(*args, **kwargs)
        bs_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(bs, bs_c, 12)
        args = [a, sfreq, None, 8, None, fl, 1.0]
        lp = filter_data(*args, **kwargs)
        lp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(lp, lp_c, 12)
        args = [lp, sfreq, 4, None, None, fl, 1.0]
        hp = filter_data(*args, **kwargs)
        hp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(hp, hp_c, 12)
out = log_file.getvalue().split('\n')[:-1]
from mne.cuda import _cuda_capable
tot = 12 if _cuda_capable else 0
assert sum(['Using CUDA for FFT FIR filtering' in o for o in out]) == tot
if not _cuda_capable:
    pytest.skip('CUDA not enabled')
```

## Next Steps


---

*Source: test_filter.py:803 | Complexity: Advanced | Last updated: 2026-05-18*