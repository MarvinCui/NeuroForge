# How To: Persyst Raw

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading Persyst files using path to header file.

## Prerequisites

**Required Modules:**
- `os`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test reading Persyst files using path to header file.'

```python
'Test reading Persyst files using path to header file.'
```

**Verification:**
```python
assert data.shape == (83, 647)
```

### Step 2: Assign raw = read_raw_persyst(...)

```python
raw = read_raw_persyst(fname_lay, preload=False)
```

**Verification:**
```python
assert times.min() == 1.0
```

### Step 3: Assign raw = raw.pick(...)

```python
raw = raw.pick('eeg')
```

**Verification:**
```python
assert times.max() == 4.23
```

### Step 4: Assign unknown = raw.get_data(...)

```python
data, times = raw.get_data(start=200, return_times=True)
```

**Verification:**
```python
assert data.shape == (83, 200)
```

### Step 5: Assign data = raw.get_data(...)

```python
data = raw.get_data(start=200, stop=400)
```

**Verification:**
```python
assert not data.min() == 0 and (not data.max() == 0)
```

### Step 6: Assign first_ch_data = raw.get_data(...)

```python
first_ch_data = raw.get_data(picks=[0], start=200, stop=400)
```

**Verification:**
```python
assert_array_equal(first_ch_data.squeeze(), data[0, :])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(first_ch_data.squeeze(), data[0, :])
```


## Complete Example

```python
# Workflow
'Test reading Persyst files using path to header file.'
raw = read_raw_persyst(fname_lay, preload=False)
raw = raw.pick('eeg')
data, times = raw.get_data(start=200, return_times=True)
assert data.shape == (83, 647)
assert times.min() == 1.0
assert times.max() == 4.23
data = raw.get_data(start=200, stop=400)
assert data.shape == (83, 200)
assert not data.min() == 0 and (not data.max() == 0)
first_ch_data = raw.get_data(picks=[0], start=200, stop=400)
assert_array_equal(first_ch_data.squeeze(), data[0, :])
```

## Next Steps


---

*Source: test_persyst.py:52 | Complexity: Intermediate | Last updated: 2026-05-18*