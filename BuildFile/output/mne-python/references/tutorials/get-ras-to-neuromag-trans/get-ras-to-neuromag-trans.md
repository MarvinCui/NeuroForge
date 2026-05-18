# How To: Get Ras To Neuromag Trans

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the coordinate transformation from ras to neuromag.

## Prerequisites

**Required Modules:**
- `itertools`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.transforms`
- `mne.transforms`
- `dipy.align`


## Step-by-Step Guide

### Step 1: 'Test the coordinate transformation from ras to neuromag.'

```python
'Test the coordinate transformation from ras to neuromag.'
```

**Verification:**
```python
assert_allclose(pts_restored, pts, atol=1e-06, err_msg=err)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 3: Assign anterior = value

```python
anterior = [0, 1, 0]
```

### Step 4: Assign left = value

```python
left = [-1, 0, 0]
```

### Step 5: Assign right = value

```python
right = [0.8, 0, 0]
```

### Step 6: Assign up = value

```python
up = [0, 0, 1]
```

### Step 7: Assign rand_pts = rng.uniform(...)

```python
rand_pts = rng.uniform(-1, 1, (3, 3))
```

### Step 8: Assign pts = np.vstack(...)

```python
pts = np.vstack((anterior, left, right, up, rand_pts))
```

### Step 9: Assign unknown = rng.uniform(...)

```python
rx, ry, rz, tx, ty, tz = rng.uniform(-2 * np.pi, 2 * np.pi, 6)
```

### Step 10: Assign trans = np.dot(...)

```python
trans = np.dot(translation(tx, ty, tz), rotation(rx, ry, rz))
```

### Step 11: Assign pts_changed = apply_trans(...)

```python
pts_changed = apply_trans(trans, pts)
```

### Step 12: Assign unknown = value

```python
nas, lpa, rpa = pts_changed[:3]
```

### Step 13: Assign hsp_trans = get_ras_to_neuromag_trans(...)

```python
hsp_trans = get_ras_to_neuromag_trans(nas, lpa, rpa)
```

### Step 14: Assign pts_restored = apply_trans(...)

```python
pts_restored = apply_trans(hsp_trans, pts_changed)
```

### Step 15: Assign err = 'Neuromag transformation failed'

```python
err = 'Neuromag transformation failed'
```

### Step 16: Call assert_allclose()

```python
assert_allclose(pts_restored, pts, atol=1e-06, err_msg=err)
```


## Complete Example

```python
# Workflow
'Test the coordinate transformation from ras to neuromag.'
rng = np.random.RandomState(0)
anterior = [0, 1, 0]
left = [-1, 0, 0]
right = [0.8, 0, 0]
up = [0, 0, 1]
rand_pts = rng.uniform(-1, 1, (3, 3))
pts = np.vstack((anterior, left, right, up, rand_pts))
rx, ry, rz, tx, ty, tz = rng.uniform(-2 * np.pi, 2 * np.pi, 6)
trans = np.dot(translation(tx, ty, tz), rotation(rx, ry, rz))
pts_changed = apply_trans(trans, pts)
nas, lpa, rpa = pts_changed[:3]
hsp_trans = get_ras_to_neuromag_trans(nas, lpa, rpa)
pts_restored = apply_trans(hsp_trans, pts_changed)
err = 'Neuromag transformation failed'
assert_allclose(pts_restored, pts, atol=1e-06, err_msg=err)
```

## Next Steps


---

*Source: test_transforms.py:131 | Complexity: Advanced | Last updated: 2026-05-18*