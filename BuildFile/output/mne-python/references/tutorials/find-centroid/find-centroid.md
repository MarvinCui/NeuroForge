# How To: Find Centroid

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the centroid is correct.

## Prerequisites

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `mne`
- `mne.channels`
- `mne.preprocessing`
- `mne.preprocessing.interpolate`
- `mne.transforms`


## Step-by-Step Guide

### Step 1: 'Test that the centroid is correct.'

```python
'Test that the centroid is correct.'
```

**Verification:**
```python
assert pos['coord_frame'] == 'head'
```

### Step 2: Assign montage = make_standard_montage(...)

```python
montage = make_standard_montage('standard_1020')
```

### Step 3: Assign ch_names = value

```python
ch_names = [ch for ch in montage.ch_names if ch not in ['P7', 'P8', 'T3', 'T4', 'T5', 'T4', 'T6']]
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(ch_names, sfreq=1024, ch_types='eeg')
```

### Step 5: Call info.set_montage()

```python
info.set_montage(montage)
```

### Step 6: Assign montage = info.get_montage(...)

```python
montage = info.get_montage()
```

### Step 7: Assign pos = montage.get_positions(...)

```python
pos = montage.get_positions()
```

**Verification:**
```python
assert pos['coord_frame'] == 'head'
```

### Step 8: Assign ch_names = value

```python
ch_names = ['T7', 'TP7']
```

### Step 9: Assign pos_centroid = _find_centroid_sphere(...)

```python
pos_centroid = _find_centroid_sphere(pos['ch_pos'], ch_names)
```

### Step 10: Call _check_centroid_position()

```python
_check_centroid_position(pos, ch_names, pos_centroid)
```

### Step 11: Assign pairs = value

```python
pairs = [('CPz', 'CP2'), ('CPz', 'Cz'), ('Fpz', 'AFz'), ('AF7', 'F7'), ('O1', 'O2'), ('M2', 'A2'), ('P5', 'P9')]
```

### Step 12: Assign triplets = value

```python
triplets = [('CPz', 'Cz', 'FCz'), ('AF9', 'Fpz', 'AF10'), ('FT10', 'FT8', 'T10')]
```

### Step 13: Assign pos_centroid = _find_centroid_sphere(...)

```python
pos_centroid = _find_centroid_sphere(pos['ch_pos'], ch_names)
```

### Step 14: Call _check_centroid_position()

```python
_check_centroid_position(pos, ch_names, pos_centroid)
```

### Step 15: Assign pos_centroid = _find_centroid_sphere(...)

```python
pos_centroid = _find_centroid_sphere(pos['ch_pos'], ch_names)
```

### Step 16: Call _check_centroid_position()

```python
_check_centroid_position(pos, ch_names, pos_centroid)
```


## Complete Example

```python
# Workflow
'Test that the centroid is correct.'
montage = make_standard_montage('standard_1020')
ch_names = [ch for ch in montage.ch_names if ch not in ['P7', 'P8', 'T3', 'T4', 'T5', 'T4', 'T6']]
info = create_info(ch_names, sfreq=1024, ch_types='eeg')
info.set_montage(montage)
montage = info.get_montage()
pos = montage.get_positions()
assert pos['coord_frame'] == 'head'
ch_names = ['T7', 'TP7']
pos_centroid = _find_centroid_sphere(pos['ch_pos'], ch_names)
_check_centroid_position(pos, ch_names, pos_centroid)
pairs = [('CPz', 'CP2'), ('CPz', 'Cz'), ('Fpz', 'AFz'), ('AF7', 'F7'), ('O1', 'O2'), ('M2', 'A2'), ('P5', 'P9')]
for ch_names in pairs:
    pos_centroid = _find_centroid_sphere(pos['ch_pos'], ch_names)
    _check_centroid_position(pos, ch_names, pos_centroid)
triplets = [('CPz', 'Cz', 'FCz'), ('AF9', 'Fpz', 'AF10'), ('FT10', 'FT8', 'T10')]
for ch_names in triplets:
    pos_centroid = _find_centroid_sphere(pos['ch_pos'], ch_names)
    _check_centroid_position(pos, ch_names, pos_centroid)
```

## Next Steps


---

*Source: test_interpolate.py:147 | Complexity: Advanced | Last updated: 2026-05-18*