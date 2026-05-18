# How To: Gdf Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading raw GDF 1.x files.

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

### Step 1: 'Test reading raw GDF 1.x files.'

```python
'Test reading raw GDF 1.x files.'
```

**Verification:**
```python
assert_array_equal(evs[:, 0], EXPECTED_EVS_ONSETS)
```

### Step 2: Assign raw = read_raw_gdf(...)

```python
raw = read_raw_gdf(gdf1_path.with_name(gdf1_path.name + '.gdf'), eog=None, misc=None, preload=True)
```

**Verification:**
```python
assert evs_id == EXPECTED_EVS_ID
```

### Step 3: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=False, eeg=True, exclude='bads')
```

**Verification:**
```python
assert_allclose(data, data_biosig, rtol=1e-08)
```

### Step 4: Assign unknown = value

```python
data, _ = raw[picks]
```

**Verification:**
```python
assert len(raw.annotations.duration == 963)
```

### Step 5: Assign EXPECTED_EVS_ONSETS = value

```python
EXPECTED_EVS_ONSETS = raw._raw_extras[0]['events'][1]
```

**Verification:**
```python
assert raw.info['meas_date'] is None
```

### Step 6: Assign EXPECTED_EVS_ID = value

```python
EXPECTED_EVS_ID = {f'{evs}': i for i, evs in enumerate([32769, 32770, 33024, 33025, 33026, 33027, 33028, 33029, 33040, 33041, 33042, 33043, 33044, 33045, 33285, 33286], 1)}
```

### Step 7: Assign unknown = events_from_annotations(...)

```python
evs, evs_id = events_from_annotations(raw)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(evs[:, 0], EXPECTED_EVS_ONSETS)
```

**Verification:**
```python
assert evs_id == EXPECTED_EVS_ID
```

### Step 9: Assign raw_biosig = np.load(...)

```python
raw_biosig = np.load(gdf1_path.with_name(gdf1_path.name + '_biosig.npy'))
```

### Step 10: Assign raw_biosig = value

```python
raw_biosig = raw_biosig * 1e-06
```

### Step 11: Assign data_biosig = value

```python
data_biosig = raw_biosig[picks]
```

### Step 12: Call assert_allclose()

```python
assert_allclose(data, data_biosig, rtol=1e-08)
```

**Verification:**
```python
assert len(raw.annotations.duration == 963)
```


## Complete Example

```python
# Workflow
'Test reading raw GDF 1.x files.'
raw = read_raw_gdf(gdf1_path.with_name(gdf1_path.name + '.gdf'), eog=None, misc=None, preload=True)
picks = pick_types(raw.info, meg=False, eeg=True, exclude='bads')
data, _ = raw[picks]
EXPECTED_EVS_ONSETS = raw._raw_extras[0]['events'][1]
EXPECTED_EVS_ID = {f'{evs}': i for i, evs in enumerate([32769, 32770, 33024, 33025, 33026, 33027, 33028, 33029, 33040, 33041, 33042, 33043, 33044, 33045, 33285, 33286], 1)}
evs, evs_id = events_from_annotations(raw)
assert_array_equal(evs[:, 0], EXPECTED_EVS_ONSETS)
assert evs_id == EXPECTED_EVS_ID
raw_biosig = np.load(gdf1_path.with_name(gdf1_path.name + '_biosig.npy'))
raw_biosig = raw_biosig * 1e-06
data_biosig = raw_biosig[picks]
assert_allclose(data, data_biosig, rtol=1e-08)
assert len(raw.annotations.duration == 963)
assert raw.info['meas_date'] is None
```

## Next Steps


---

*Source: test_gdf.py:26 | Complexity: Advanced | Last updated: 2026-05-18*