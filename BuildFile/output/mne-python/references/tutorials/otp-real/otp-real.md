# How To: Otp Real

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test OTP on real data.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.fft`
- `mne`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test OTP on real data.'

```python
'Test OTP on real data.'
```

**Verification:**
```python
assert reduction.min() > 1
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(skip_fname, preload=True)
```

### Step 3: Call raw.pick()

```python
raw.pick(raw.ch_names[:10])
```

### Step 4: Assign raw_otp = oversampled_temporal_projection(...)

```python
raw_otp = oversampled_temporal_projection(raw, duration=1.0)
```

### Step 5: Assign raw = read_raw_fif.crop(...)

```python
raw = read_raw_fif(fname, allow_maxshield='yes').crop(0, 1)
```

### Step 6: Call raw.load_data.pick()

```python
raw.load_data().pick(raw.ch_names[:10])
```

### Step 7: Assign raw_otp = oversampled_temporal_projection(...)

```python
raw_otp = oversampled_temporal_projection(raw, 1.0)
```

### Step 8: Assign picks = _pick_data_channels(...)

```python
picks = _pick_data_channels(raw.info)
```

### Step 9: Assign reduction = value

```python
reduction = np.linalg.norm(raw[picks][0], axis=-1) / np.linalg.norm(raw_otp[picks][0], axis=-1)
```

**Verification:**
```python
assert reduction.min() > 1
```


## Complete Example

```python
# Workflow
'Test OTP on real data.'
for fname in (erm_fname, triux_fname):
    raw = read_raw_fif(fname, allow_maxshield='yes').crop(0, 1)
    raw.load_data().pick(raw.ch_names[:10])
    raw_otp = oversampled_temporal_projection(raw, 1.0)
    picks = _pick_data_channels(raw.info)
    reduction = np.linalg.norm(raw[picks][0], axis=-1) / np.linalg.norm(raw_otp[picks][0], axis=-1)
    assert reduction.min() > 1
raw = read_raw_fif(skip_fname, preload=True)
raw.pick(raw.ch_names[:10])
raw_otp = oversampled_temporal_projection(raw, duration=1.0)
```

## Next Steps


---

*Source: test_otp.py:84 | Complexity: Advanced | Last updated: 2026-05-18*