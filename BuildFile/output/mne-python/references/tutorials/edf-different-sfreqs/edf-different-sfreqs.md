# How To: Edf Different Sfreqs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test EDF with various sampling rates.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `contextlib`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.edf.edf`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: stim_channel
```

## Step-by-Step Guide

### Step 1: 'Test EDF with various sampling rates.'

```python
'Test EDF with various sampling rates.'
```

**Verification:**
```python
assert_allclose(data1, data2, err_msg='Data mismatch with preload')
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(times1, times2)
```

### Step 3: Assign raw1 = read_raw_edf(...)

```python
raw1 = read_raw_edf(input_fname=edf_reduced, stim_channel=stim_channel, verbose='error', preload=False)
```

**Verification:**
```python
assert_allclose(data1, data2, err_msg='Data mismatch with preload')
```

### Step 4: Assign raw2 = read_raw_edf(...)

```python
raw2 = read_raw_edf(input_fname=edf_reduced, stim_channel=stim_channel, verbose='error', preload=True)
```

**Verification:**
```python
assert_allclose(times1, times2)
```

### Step 5: Assign picks = value

```python
picks = rng.permutation(np.arange(len(raw1.ch_names) - 1))[:10]
```

### Step 6: Assign unknown = value

```python
data1, times1 = raw1[picks, :]
```

### Step 7: Assign unknown = value

```python
data2, times2 = raw2[picks, :]
```

### Step 8: Call assert_allclose()

```python
assert_allclose(data1, data2, err_msg='Data mismatch with preload')
```

### Step 9: Call assert_allclose()

```python
assert_allclose(times1, times2)
```

### Step 10: Assign unknown = value

```python
data2, times2 = raw2[picks, :512]
```

### Step 11: Assign picks = np.arange(...)

```python
picks = np.arange(15, 20)
```

### Step 12: Assign unknown = value

```python
data1, times1 = raw1[picks, :512]
```

### Step 13: Assign unknown = value

```python
data2, times2 = raw2[picks, :512]
```

### Step 14: Call assert_allclose()

```python
assert_allclose(data1, data2, err_msg='Data mismatch with preload')
```

### Step 15: Call assert_allclose()

```python
assert_allclose(times1, times2)
```

### Step 16: Assign unknown = value

```python
data1, times1 = raw1[picks, :512]
```


## Complete Example

```python
# Setup
# Fixtures: stim_channel

# Workflow
'Test EDF with various sampling rates.'
rng = np.random.RandomState(0)
raw1 = read_raw_edf(input_fname=edf_reduced, stim_channel=stim_channel, verbose='error', preload=False)
raw2 = read_raw_edf(input_fname=edf_reduced, stim_channel=stim_channel, verbose='error', preload=True)
picks = rng.permutation(np.arange(len(raw1.ch_names) - 1))[:10]
data1, times1 = raw1[picks, :]
data2, times2 = raw2[picks, :]
assert_allclose(data1, data2, err_msg='Data mismatch with preload')
assert_allclose(times1, times2)
with pytest.warns(RuntimeWarning, match='mixed sampling frequencies'):
    data1, times1 = raw1[picks, :512]
data2, times2 = raw2[picks, :512]
picks = np.arange(15, 20)
data1, times1 = raw1[picks, :512]
data2, times2 = raw2[picks, :512]
assert_allclose(data1, data2, err_msg='Data mismatch with preload')
assert_allclose(times1, times2)
```

## Next Steps


---

*Source: test_edf.py:225 | Complexity: Advanced | Last updated: 2026-05-18*