# How To: Get Montage Volume Labels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test finding ROI labels near montage channel locations.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test finding ROI labels near montage channel locations.'

```python
'Test finding ROI labels near montage channel locations.'
```

**Verification:**
```python
assert labels == {'1': ['Unknown'], '2': ['Left-Cerebral-Cortex'], '3': ['Left-Cerebral-Cortex']}
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert 'Unknown' in colors
```

### Step 3: Assign ch_coords = np.array(...)

```python
ch_coords = np.array([[-8.7040273, 17.99938754, 10.29604017], [-14.03007764, 19.69978401, 12.07236939], [-21.1130506, 21.98310911, 13.25658887]])
```

**Verification:**
```python
assert 'Left-Cerebral-Cortex' in colors
```

### Step 4: Assign ch_pos = dict(...)

```python
ch_pos = dict(zip(['1', '2', '3'], ch_coords / 1000))
```

### Step 5: Assign montage = make_dig_montage(...)

```python
montage = make_dig_montage(ch_pos, coord_frame='mri')
```

### Step 6: Assign unknown = get_montage_volume_labels(...)

```python
labels, colors = get_montage_volume_labels(montage, 'sample', subjects_dir, aseg='aseg', dist=1)
```

**Verification:**
```python
assert labels == {'1': ['Unknown'], '2': ['Left-Cerebral-Cortex'], '3': ['Left-Cerebral-Cortex']}
```

### Step 7: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(colors['Left-Cerebral-Cortex'], (0.803921568627451, 0.24313725490196078, 0.3058823529411765, 1.0))
```

### Step 8: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(colors['Unknown'], (0.0, 0.0, 0.0, 1.0))
```

### Step 9: Assign fail_montage = make_dig_montage(...)

```python
fail_montage = make_dig_montage(ch_pos, coord_frame='head')
```

### Step 10: Call get_montage_volume_labels()

```python
get_montage_volume_labels(fail_montage, 'sample', subjects_dir, aseg='aseg')
```

### Step 11: Call get_montage_volume_labels()

```python
get_montage_volume_labels(montage, 'sample', subjects_dir, dist=11)
```


## Complete Example

```python
# Workflow
'Test finding ROI labels near montage channel locations.'
pytest.importorskip('nibabel')
ch_coords = np.array([[-8.7040273, 17.99938754, 10.29604017], [-14.03007764, 19.69978401, 12.07236939], [-21.1130506, 21.98310911, 13.25658887]])
ch_pos = dict(zip(['1', '2', '3'], ch_coords / 1000))
montage = make_dig_montage(ch_pos, coord_frame='mri')
labels, colors = get_montage_volume_labels(montage, 'sample', subjects_dir, aseg='aseg', dist=1)
assert labels == {'1': ['Unknown'], '2': ['Left-Cerebral-Cortex'], '3': ['Left-Cerebral-Cortex']}
assert 'Unknown' in colors
assert 'Left-Cerebral-Cortex' in colors
np.testing.assert_almost_equal(colors['Left-Cerebral-Cortex'], (0.803921568627451, 0.24313725490196078, 0.3058823529411765, 1.0))
np.testing.assert_almost_equal(colors['Unknown'], (0.0, 0.0, 0.0, 1.0))
fail_montage = make_dig_montage(ch_pos, coord_frame='head')
with pytest.raises(RuntimeError, match='Coordinate frame not supported'):
    get_montage_volume_labels(fail_montage, 'sample', subjects_dir, aseg='aseg')
with pytest.raises(ValueError, match='between 0 and 10'):
    get_montage_volume_labels(montage, 'sample', subjects_dir, dist=11)
```

## Next Steps


---

*Source: test_surface.py:285 | Complexity: Advanced | Last updated: 2026-05-18*