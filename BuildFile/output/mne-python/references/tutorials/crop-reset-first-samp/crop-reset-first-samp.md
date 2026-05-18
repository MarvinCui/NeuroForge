# How To: Crop Reset First Samp

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Regression test for GH-13278.

crop(reset_first_samp=True) must reset first_samp to 0.

## Prerequisites

**Required Modules:**
- `math`
- `os`
- `re`
- `contextlib`
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne._fiff.utils`
- `mne.io`
- `mne.io.base`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Regression test for GH-13278.\n\n    crop(reset_first_samp=True) must reset first_samp to 0.\n    '

```python
'Regression test for GH-13278.\n\n    crop(reset_first_samp=True) must reset first_samp to 0.\n    '
```

**Verification:**
```python
assert raw.first_samp == 0
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(ch_names=['CH1'], sfreq=1000.0, ch_types=['eeg'])
```

**Verification:**
```python
assert raw.times[0] == 0.0
```

### Step 3: Assign data = np.zeros(...)

```python
data = np.zeros((1, 10000))
```

**Verification:**
```python
assert raw2.first_samp != 0
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 5: Call raw.crop()

```python
raw.crop(tmin=2.0, tmax=5.0, reset_first_samp=True)
```

**Verification:**
```python
assert raw.first_samp == 0
```

### Step 6: Assign raw2 = RawArray(...)

```python
raw2 = RawArray(data, info)
```

### Step 7: Call raw2.crop()

```python
raw2.crop(tmin=2.0, tmax=5.0)
```

**Verification:**
```python
assert raw2.first_samp != 0
```


## Complete Example

```python
# Workflow
'Regression test for GH-13278.\n\n    crop(reset_first_samp=True) must reset first_samp to 0.\n    '
info = create_info(ch_names=['CH1'], sfreq=1000.0, ch_types=['eeg'])
data = np.zeros((1, 10000))
raw = RawArray(data, info)
raw.crop(tmin=2.0, tmax=5.0, reset_first_samp=True)
assert raw.first_samp == 0
assert raw.times[0] == 0.0
raw2 = RawArray(data, info)
raw2.crop(tmin=2.0, tmax=5.0)
assert raw2.first_samp != 0
```

## Next Steps


---

*Source: test_raw.py:1104 | Complexity: Intermediate | Last updated: 2026-05-18*