# How To: Make Field Map Meeg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test making a M/EEG field map onto helmet & head.

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.polynomial`
- `numpy.testing`
- `scipy.interpolate`
- `mne`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.forward`
- `mne.forward._field_interpolation`
- `mne.forward._lead_dots`
- `mne.forward._make_forward`
- `mne.io`
- `mne.surface`


## Step-by-Step Guide

### Step 1: 'Test making a M/EEG field map onto helmet & head.'

```python
'Test making a M/EEG field map onto helmet & head.'
```

**Verification:**
```python
assert_equal(maps[0]['data'].shape, (642, 6))
```

### Step 2: Assign evoked = value

```python
evoked = read_evokeds(evoked_fname, baseline=(-0.2, 0.0))[0]
```

**Verification:**
```python
assert_equal(maps[1]['data'].shape, (304, 31))
```

### Step 3: Assign picks = pick_types(...)

```python
picks = pick_types(evoked.info, meg=True, eeg=True)
```

**Verification:**
```python
assert_equal(len(maxs), len(maps))
```

### Step 4: Assign picks = value

```python
picks = picks[::10]
```

**Verification:**
```python
assert_allclose(map_['data'].max(), max_, rtol=0.05)
```

### Step 5: Call evoked.pick()

```python
evoked.pick([evoked.ch_names[p] for p in picks])
```

**Verification:**
```python
assert_allclose(map_['data'].min(), min_, rtol=0.05)
```

### Step 6: Call evoked.info.normalize_proj()

```python
evoked.info.normalize_proj()
```

**Verification:**
```python
assert_allclose(np.sqrt(np.sum(maps[0]['data'] ** 2)), 19.0903, atol=0.001, rtol=0.001)
```

### Step 7: Assign maps = make_field_map(...)

```python
maps = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, verbose='debug', origin=(0.0, 0.0, 0.04))
```

**Verification:**
```python
assert_allclose(np.sqrt(np.sum(maps[1]['data'] ** 2)), 19.4748, atol=0.001, rtol=0.001)
```

### Step 8: Call assert_equal()

```python
assert_equal(maps[0]['data'].shape, (642, 6))
```

### Step 9: Call assert_equal()

```python
assert_equal(maps[1]['data'].shape, (304, 31))
```

### Step 10: Assign maxs = value

```python
maxs = (1.2, 2.0)
```

### Step 11: Assign mins = value

```python
mins = (-0.8, -1.3)
```

### Step 12: Call assert_equal()

```python
assert_equal(len(maxs), len(maps))
```

### Step 13: Call assert_allclose()

```python
assert_allclose(np.sqrt(np.sum(maps[0]['data'] ** 2)), 19.0903, atol=0.001, rtol=0.001)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(np.sqrt(np.sum(maps[1]['data'] ** 2)), 19.4748, atol=0.001, rtol=0.001)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(map_['data'].max(), max_, rtol=0.05)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(map_['data'].min(), min_, rtol=0.05)
```


## Complete Example

```python
# Workflow
'Test making a M/EEG field map onto helmet & head.'
evoked = read_evokeds(evoked_fname, baseline=(-0.2, 0.0))[0]
picks = pick_types(evoked.info, meg=True, eeg=True)
picks = picks[::10]
evoked.pick([evoked.ch_names[p] for p in picks])
evoked.info.normalize_proj()
maps = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, verbose='debug', origin=(0.0, 0.0, 0.04))
assert_equal(maps[0]['data'].shape, (642, 6))
assert_equal(maps[1]['data'].shape, (304, 31))
maxs = (1.2, 2.0)
mins = (-0.8, -1.3)
assert_equal(len(maxs), len(maps))
for map_, max_, min_ in zip(maps, maxs, mins):
    assert_allclose(map_['data'].max(), max_, rtol=0.05)
    assert_allclose(map_['data'].min(), min_, rtol=0.05)
assert_allclose(np.sqrt(np.sum(maps[0]['data'] ** 2)), 19.0903, atol=0.001, rtol=0.001)
assert_allclose(np.sqrt(np.sum(maps[1]['data'] ** 2)), 19.4748, atol=0.001, rtol=0.001)
```

## Next Steps


---

*Source: test_field_interpolation.py:235 | Complexity: Advanced | Last updated: 2026-05-18*