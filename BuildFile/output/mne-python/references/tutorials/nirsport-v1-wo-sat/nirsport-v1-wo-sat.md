# How To: Nirsport V1 Wo Sat

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test NIRSport1 file with no saturation.

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

### Step 1: 'Test NIRSport1 file with no saturation.'

```python
'Test NIRSport1 file with no saturation.'
```

**Verification:**
```python
assert raw._data.shape == (26, 164)
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(nirsport1_wo_sat, preload=True)
```

**Verification:**
```python
assert raw.info['sfreq'] == 10.416667
```

### Step 3: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(nirsport1_wo_sat, preload=True, saturated='nan')
```

**Verification:**
```python
assert np.sum(np.isnan(raw.get_data())) == 0
```

### Step 4: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert data.shape == (26, 164)
```

### Step 5: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(nirsport1_wo_sat, saturated='annotate')
```

**Verification:**
```python
assert np.sum(np.isnan(data)) == 0
```

### Step 6: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert data.shape == (26, 164)
```


## Complete Example

```python
# Workflow
'Test NIRSport1 file with no saturation.'
raw = read_raw_nirx(nirsport1_wo_sat, preload=True)
assert raw._data.shape == (26, 164)
assert raw.info['sfreq'] == 10.416667
assert np.sum(np.isnan(raw.get_data())) == 0
raw = read_raw_nirx(nirsport1_wo_sat, preload=True, saturated='nan')
data = raw.get_data()
assert data.shape == (26, 164)
assert np.sum(np.isnan(data)) == 0
raw = read_raw_nirx(nirsport1_wo_sat, saturated='annotate')
data = raw.get_data()
assert data.shape == (26, 164)
assert np.sum(np.isnan(data)) == 0
```

## Next Steps


---

*Source: test_nirx.py:147 | Complexity: Intermediate | Last updated: 2026-05-18*