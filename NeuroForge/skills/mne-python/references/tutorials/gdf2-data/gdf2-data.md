# How To: Gdf2 Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading raw GDF 2.x files.

## Prerequisites

**Required Modules:**
- `shutil`
- `datetime`
- `io`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test reading raw GDF 2.x files.'

```python
'Test reading raw GDF 2.x files.'
```

**Verification:**
```python
assert raw.info['subject_info']['birthday'] == date(1, 1, 1)
```

### Step 2: Assign raw = read_raw_gdf(...)

```python
raw = read_raw_gdf(gdf2_path.with_name(gdf2_path.name + '.gdf'), eog=None, misc=None, preload=True)
```

**Verification:**
```python
assert_allclose(data, data_biosig, rtol=1e-08)
```

### Step 3: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=False, eeg=True, exclude='bads')
```

**Verification:**
```python
assert_equal(events.shape[0], 2)
```

### Step 4: Assign unknown = value

```python
data, _ = raw[picks]
```

**Verification:**
```python
assert_array_equal(events[:, 2], [20, 28])
```

### Step 5: Assign mat = sio.loadmat(...)

```python
mat = sio.loadmat(gdf2_path.with_name(gdf2_path.name + '_biosig.mat'))
```

**Verification:**
```python
assert raw.info['meas_date'] is None
```

### Step 6: Assign data_biosig = value

```python
data_biosig = mat['dat'] * 1e-06
```

### Step 7: Assign data_biosig = value

```python
data_biosig = data_biosig[picks]
```

### Step 8: Call assert_allclose()

```python
assert_allclose(data, data_biosig, rtol=1e-08)
```

### Step 9: Assign events = find_events(...)

```python
events = find_events(raw, verbose=1)
```

### Step 10: Call assert_equal()

```python
assert_equal(events.shape[0], 2)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(events[:, 2], [20, 28])
```

**Verification:**
```python
assert raw.info['meas_date'] is None
```

### Step 12: Call _test_raw_reader()

```python
_test_raw_reader(read_raw_gdf, input_fname=gdf2_path.with_name(gdf2_path.name + '.gdf'), eog=None, misc=None, test_scaling=False)
```


## Complete Example

```python
# Workflow
'Test reading raw GDF 2.x files.'
raw = read_raw_gdf(gdf2_path.with_name(gdf2_path.name + '.gdf'), eog=None, misc=None, preload=True)
assert raw.info['subject_info']['birthday'] == date(1, 1, 1)
picks = pick_types(raw.info, meg=False, eeg=True, exclude='bads')
data, _ = raw[picks]
mat = sio.loadmat(gdf2_path.with_name(gdf2_path.name + '_biosig.mat'))
data_biosig = mat['dat'] * 1e-06
data_biosig = data_biosig[picks]
assert_allclose(data, data_biosig, rtol=1e-08)
events = find_events(raw, verbose=1)
events[:, 2] >>= 8
assert_equal(events.shape[0], 2)
assert_array_equal(events[:, 2], [20, 28])
assert raw.info['meas_date'] is None
_test_raw_reader(read_raw_gdf, input_fname=gdf2_path.with_name(gdf2_path.name + '.gdf'), eog=None, misc=None, test_scaling=False)
```

## Next Steps


---

*Source: test_gdf.py:113 | Complexity: Advanced | Last updated: 2026-05-18*