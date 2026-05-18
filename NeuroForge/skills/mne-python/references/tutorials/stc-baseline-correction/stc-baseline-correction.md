# How To: Stc Baseline Correction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test baseline correction for source estimate objects.

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `contextlib`
- `copy`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy`
- `scipy.optimize`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.morph_map`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test baseline correction for source estimate objects.'

```python
'Test baseline correction for source estimate objects.'
```

**Verification:**
```python
assert_array_almost_equal(mean_base, zero_array)
```

### Step 2: Assign stcs = value

```python
stcs = [read_source_estimate(fname_stc), read_source_estimate(fname_vol, 'sample')]
```

### Step 3: Assign baselines = value

```python
baselines = [(0.0, 0.1), (None, None)]
```

### Step 4: Assign times = value

```python
times = stc.times
```

### Step 5: Assign stc = stc.apply_baseline(...)

```python
stc = stc.apply_baseline(baseline=(start, stop))
```

### Step 6: Assign t0 = value

```python
t0 = start or stc.times[0]
```

### Step 7: Assign t1 = value

```python
t1 = stop or stc.times[-1]
```

### Step 8: Assign imin = np.abs.argmin(...)

```python
imin = np.abs(times - t0).argmin()
```

### Step 9: Assign imax = value

```python
imax = np.abs(times - t1).argmin() + 1
```

### Step 10: Assign data_base = value

```python
data_base = stc.data[:, imin:imax]
```

### Step 11: Assign mean_base = data_base.mean(...)

```python
mean_base = data_base.mean(axis=1)
```

### Step 12: Assign zero_array = np.zeros(...)

```python
zero_array = np.zeros(mean_base.shape[0])
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(mean_base, zero_array)
```


## Complete Example

```python
# Workflow
'Test baseline correction for source estimate objects.'
stcs = [read_source_estimate(fname_stc), read_source_estimate(fname_vol, 'sample')]
baselines = [(0.0, 0.1), (None, None)]
for stc in stcs:
    times = stc.times
    for start, stop in baselines:
        stc = stc.apply_baseline(baseline=(start, stop))
        t0 = start or stc.times[0]
        t1 = stop or stc.times[-1]
        imin = np.abs(times - t0).argmin()
        imax = np.abs(times - t1).argmin() + 1
        data_base = stc.data[:, imin:imax]
        mean_base = data_base.mean(axis=1)
        zero_array = np.zeros(mean_base.shape[0])
        assert_array_almost_equal(mean_base, zero_array)
```

## Next Steps


---

*Source: test_source_estimate.py:119 | Complexity: Advanced | Last updated: 2026-05-18*