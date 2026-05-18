# How To: Stc Snr

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test computing SNR from a STC.

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

### Step 1: 'Test computing SNR from a STC.'

```python
'Test computing SNR from a STC.'
```

**Verification:**
```python
assert (stc.data < 0).any()
```

### Step 2: Assign inv = read_inverse_operator(...)

```python
inv = read_inverse_operator(fname_inv_fixed)
```

**Verification:**
```python
assert_allclose(snr.times, evoked.times)
```

### Step 3: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_fwd)
```

**Verification:**
```python
assert snr.max() < -10
```

### Step 4: Assign cov = read_cov(...)

```python
cov = read_cov(fname_cov)
```

**Verification:**
```python
assert snr.min() > -120
```

### Step 5: Assign evoked = unknown.crop(...)

```python
evoked = read_evokeds(fname_evoked, baseline=(None, 0))[0].crop(0, 0.01)
```

### Step 6: Assign stc = apply_inverse(...)

```python
stc = apply_inverse(evoked, inv)
```

**Verification:**
```python
assert (stc.data < 0).any()
```

### Step 7: Assign stc = apply_inverse(...)

```python
stc = apply_inverse(evoked, inv, method='MNE')
```

### Step 8: Assign snr = stc.estimate_snr(...)

```python
snr = stc.estimate_snr(evoked.info, fwd, cov)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(snr.times, evoked.times)
```

### Step 10: Assign snr = value

```python
snr = snr.data
```

**Verification:**
```python
assert snr.max() < -10
```

### Step 11: Call stc.estimate_snr()

```python
stc.estimate_snr(evoked.info, fwd, cov)
```

### Step 12: Call abs.estimate_snr()

```python
abs(stc).estimate_snr(evoked.info, fwd, cov)
```


## Complete Example

```python
# Workflow
'Test computing SNR from a STC.'
inv = read_inverse_operator(fname_inv_fixed)
fwd = read_forward_solution(fname_fwd)
cov = read_cov(fname_cov)
evoked = read_evokeds(fname_evoked, baseline=(None, 0))[0].crop(0, 0.01)
stc = apply_inverse(evoked, inv)
assert (stc.data < 0).any()
with pytest.warns(RuntimeWarning, match='nAm'):
    stc.estimate_snr(evoked.info, fwd, cov)
with _record_warnings(), pytest.warns(RuntimeWarning, match='free ori'):
    abs(stc).estimate_snr(evoked.info, fwd, cov)
stc = apply_inverse(evoked, inv, method='MNE')
snr = stc.estimate_snr(evoked.info, fwd, cov)
assert_allclose(snr.times, evoked.times)
snr = snr.data
assert snr.max() < -10
assert snr.min() > -120
```

## Next Steps


---

*Source: test_source_estimate.py:393 | Complexity: Advanced | Last updated: 2026-05-18*