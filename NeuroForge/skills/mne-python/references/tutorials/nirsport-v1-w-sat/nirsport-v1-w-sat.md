# How To: Nirsport V1 W Sat

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test NIRSport1 file with NaNs but not in channel of interest.

## Prerequisites

**Required Modules:**
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test NIRSport1 file with NaNs but not in channel of interest.'

```python
'Test NIRSport1 file with NaNs but not in channel of interest.'
```

**Verification:**
```python
assert data.shape == (26, 176)
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(nirsport1_w_sat)
```

**Verification:**
```python
assert raw.info['sfreq'] == 10.416667
```

### Step 3: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert np.sum(np.isnan(data)) == 0
```

### Step 4: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(nirsport1_w_sat, saturated='nan')
```

**Verification:**
```python
assert data.shape == (26, 176)
```

### Step 5: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert np.sum(np.isnan(data)) == 0
```

### Step 6: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(nirsport1_w_sat, saturated='annotate')
```

**Verification:**
```python
assert data.shape == (26, 176)
```

### Step 7: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert np.sum(np.isnan(data)) == 0
```


## Complete Example

```python
# Workflow
'Test NIRSport1 file with NaNs but not in channel of interest.'
raw = read_raw_nirx(nirsport1_w_sat)
data = raw.get_data()
assert data.shape == (26, 176)
assert raw.info['sfreq'] == 10.416667
assert np.sum(np.isnan(data)) == 0
raw = read_raw_nirx(nirsport1_w_sat, saturated='nan')
data = raw.get_data()
assert data.shape == (26, 176)
assert np.sum(np.isnan(data)) == 0
raw = read_raw_nirx(nirsport1_w_sat, saturated='annotate')
data = raw.get_data()
assert data.shape == (26, 176)
assert np.sum(np.isnan(data)) == 0
```

## Next Steps


---

*Source: test_nirx.py:171 | Complexity: Intermediate | Last updated: 2026-05-18*