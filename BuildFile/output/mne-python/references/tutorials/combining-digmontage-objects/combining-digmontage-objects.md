# How To: Combining Digmontage Objects

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test combining different DigMontage objects.

## Prerequisites

**Required Modules:**
- `shutil`
- `contextlib`
- `functools`
- `itertools`
- `pathlib`
- `string`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.montage`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.channels.montage`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.io.kit`
- `mne.preprocessing`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz._3d`


## Step-by-Step Guide

### Step 1: 'Test combining different DigMontage objects.'

```python
'Test combining different DigMontage objects.'
```

**Verification:**
```python
assert repr(montage) == '<DigMontage | 6 extras (headshape), 6 HPIs, 3 fiducials, 9 channels>'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert len(montage.ch_names) == len(EXPECTED_MONTAGE.ch_names)
```

### Step 3: Assign fiducials = dict(...)

```python
fiducials = dict(zip(('nasion', 'lpa', 'rpa'), rng.rand(3, 3)))
```

**Verification:**
```python
assert all([c in montage.ch_names for c in EXPECTED_MONTAGE.ch_names])
```

### Step 4: Assign hsp1 = make_dig_montage(...)

```python
hsp1 = make_dig_montage(**fiducials, hsp=np.full((2, 3), 11.0))
```

**Verification:**
```python
assert actual_occurrences == expected_occurrences
```

### Step 5: Assign hsp2 = make_dig_montage(...)

```python
hsp2 = make_dig_montage(**fiducials, hsp=np.full((2, 3), 12.0))
```

### Step 6: Assign hsp3 = make_dig_montage(...)

```python
hsp3 = make_dig_montage(**fiducials, hsp=np.full((2, 3), 13.0))
```

### Step 7: Assign hpi1 = make_dig_montage(...)

```python
hpi1 = make_dig_montage(**fiducials, hpi=np.full((2, 3), 21.0))
```

### Step 8: Assign hpi2 = make_dig_montage(...)

```python
hpi2 = make_dig_montage(**fiducials, hpi=np.full((2, 3), 22.0))
```

### Step 9: Assign hpi3 = make_dig_montage(...)

```python
hpi3 = make_dig_montage(**fiducials, hpi=np.full((2, 3), 23.0))
```

### Step 10: Assign ch_pos1 = make_dig_montage(...)

```python
ch_pos1 = make_dig_montage(**fiducials, ch_pos={'h': [41, 41, 41], 'b': [42, 42, 42], 'g': [43, 43, 43]})
```

### Step 11: Assign ch_pos2 = make_dig_montage(...)

```python
ch_pos2 = make_dig_montage(**fiducials, ch_pos={'n': [51, 51, 51], 'y': [52, 52, 52], 'p': [53, 53, 53]})
```

### Step 12: Assign ch_pos3 = make_dig_montage(...)

```python
ch_pos3 = make_dig_montage(**fiducials, ch_pos={'v': [61, 61, 61], 'a': [62, 62, 62], 'l': [63, 63, 63]})
```

### Step 13: Assign montage = value

```python
montage = DigMontage() + hsp1 + hsp2 + hsp3 + hpi1 + hpi2 + hpi3 + ch_pos1 + ch_pos2 + ch_pos3
```

**Verification:**
```python
assert repr(montage) == '<DigMontage | 6 extras (headshape), 6 HPIs, 3 fiducials, 9 channels>'
```

### Step 14: Assign EXPECTED_MONTAGE = make_dig_montage(...)

```python
EXPECTED_MONTAGE = make_dig_montage(**fiducials, hsp=np.concatenate([np.full((2, 3), 11.0), np.full((2, 3), 12.0), np.full((2, 3), 13.0)]), hpi=np.concatenate([np.full((2, 3), 21.0), np.full((2, 3), 22.0), np.full((2, 3), 23.0)]), ch_pos={'h': [41, 41, 41], 'b': [42, 42, 42], 'g': [43, 43, 43], 'n': [51, 51, 51], 'y': [52, 52, 52], 'p': [53, 53, 53], 'v': [61, 61, 61], 'a': [62, 62, 62], 'l': [63, 63, 63]})
```

**Verification:**
```python
assert len(montage.ch_names) == len(EXPECTED_MONTAGE.ch_names)
```

### Step 15: Assign actual_occurrences = _count_points_by_type(...)

```python
actual_occurrences = _count_points_by_type(montage.dig)
```

### Step 16: Assign expected_occurrences = _count_points_by_type(...)

```python
expected_occurrences = _count_points_by_type(EXPECTED_MONTAGE.dig)
```

**Verification:**
```python
assert actual_occurrences == expected_occurrences
```


## Complete Example

```python
# Workflow
'Test combining different DigMontage objects.'
rng = np.random.RandomState(0)
fiducials = dict(zip(('nasion', 'lpa', 'rpa'), rng.rand(3, 3)))
hsp1 = make_dig_montage(**fiducials, hsp=np.full((2, 3), 11.0))
hsp2 = make_dig_montage(**fiducials, hsp=np.full((2, 3), 12.0))
hsp3 = make_dig_montage(**fiducials, hsp=np.full((2, 3), 13.0))
hpi1 = make_dig_montage(**fiducials, hpi=np.full((2, 3), 21.0))
hpi2 = make_dig_montage(**fiducials, hpi=np.full((2, 3), 22.0))
hpi3 = make_dig_montage(**fiducials, hpi=np.full((2, 3), 23.0))
ch_pos1 = make_dig_montage(**fiducials, ch_pos={'h': [41, 41, 41], 'b': [42, 42, 42], 'g': [43, 43, 43]})
ch_pos2 = make_dig_montage(**fiducials, ch_pos={'n': [51, 51, 51], 'y': [52, 52, 52], 'p': [53, 53, 53]})
ch_pos3 = make_dig_montage(**fiducials, ch_pos={'v': [61, 61, 61], 'a': [62, 62, 62], 'l': [63, 63, 63]})
montage = DigMontage() + hsp1 + hsp2 + hsp3 + hpi1 + hpi2 + hpi3 + ch_pos1 + ch_pos2 + ch_pos3
assert repr(montage) == '<DigMontage | 6 extras (headshape), 6 HPIs, 3 fiducials, 9 channels>'
EXPECTED_MONTAGE = make_dig_montage(**fiducials, hsp=np.concatenate([np.full((2, 3), 11.0), np.full((2, 3), 12.0), np.full((2, 3), 13.0)]), hpi=np.concatenate([np.full((2, 3), 21.0), np.full((2, 3), 22.0), np.full((2, 3), 23.0)]), ch_pos={'h': [41, 41, 41], 'b': [42, 42, 42], 'g': [43, 43, 43], 'n': [51, 51, 51], 'y': [52, 52, 52], 'p': [53, 53, 53], 'v': [61, 61, 61], 'a': [62, 62, 62], 'l': [63, 63, 63]})
assert len(montage.ch_names) == len(EXPECTED_MONTAGE.ch_names)
assert all([c in montage.ch_names for c in EXPECTED_MONTAGE.ch_names])
actual_occurrences = _count_points_by_type(montage.dig)
expected_occurrences = _count_points_by_type(EXPECTED_MONTAGE.dig)
assert actual_occurrences == expected_occurrences
```

## Next Steps


---

*Source: test_montage.py:880 | Complexity: Advanced | Last updated: 2026-05-18*