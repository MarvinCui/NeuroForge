# How To: Gdf Read From File Like

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that RawGDF is able to read from file-like objects for GDF files.

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

### Step 1: 'Test that RawGDF is able to read from file-like objects for GDF files.'

```python
'Test that RawGDF is able to read from file-like objects for GDF files.'
```

**Verification:**
```python
assert raw.ch_names == channels
```

### Step 2: Assign channels = unknown.split(...)

```python
channels = 'FP1 FP2 F5 AFz F6 T7 Cz T8 P7 P3 Pz P4 P8 O1 Oz O2'.split()
```

**Verification:**
```python
assert_allclose(data, data_2)
```

### Step 3: Assign fname = gdf1_path.with_name(...)

```python
fname = gdf1_path.with_name(gdf1_path.name + '.gdf')
```

**Verification:**
```python
assert raw.ch_names == channels
```

### Step 4: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

### Step 5: Assign data_2 = read_raw_gdf.get_data(...)

```python
data_2 = read_raw_gdf(fname, preload=True).get_data()
```

### Step 6: Call assert_allclose()

```python
assert_allclose(data, data_2)
```

### Step 7: Assign raw = read_raw_gdf(...)

```python
raw = read_raw_gdf(blob, preload=True)
```

### Step 8: Call read_raw_gdf()

```python
read_raw_gdf(BytesIO(), preload=True)
```


## Complete Example

```python
# Workflow
'Test that RawGDF is able to read from file-like objects for GDF files.'
channels = 'FP1 FP2 F5 AFz F6 T7 Cz T8 P7 P3 Pz P4 P8 O1 Oz O2'.split()
fname = gdf1_path.with_name(gdf1_path.name + '.gdf')
with open(fname, 'rb') as blob:
    raw = read_raw_gdf(blob, preload=True)
assert raw.ch_names == channels
data = raw.get_data()
data_2 = read_raw_gdf(fname, preload=True).get_data()
assert_allclose(data, data_2)
with pytest.raises(Exception, match='Bad GDF file provided.'):
    read_raw_gdf(BytesIO(), preload=True)
```

## Next Steps


---

*Source: test_gdf.py:189 | Complexity: Advanced | Last updated: 2026-05-18*