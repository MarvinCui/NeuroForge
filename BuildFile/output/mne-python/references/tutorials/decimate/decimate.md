# How To: Decimate

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test decimation of digitizer headshapes with too many points.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.kit.constants`
- `mne.io.kit.coreg`
- `mne.io.kit.kit`
- `mne.io.tests.test_raw`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test decimation of digitizer headshapes with too many points.'

```python
'Test decimation of digitizer headshapes with too many points.'
```

**Verification:**
```python
assert len(hsp_dec) > 5000
```

### Step 2: Assign hsp_mm = value

```python
hsp_mm = _get_ico_surface(5)['rr'] * 100
```

**Verification:**
```python
assert_array_almost_equal(hsp_rad, hsp_dec_rad, decimal=3)
```

### Step 3: Assign hsp_m = value

```python
hsp_m = hsp_mm / 1000.0
```

### Step 4: Assign sphere_hsp_path = value

```python
sphere_hsp_path = tmp_path / 'test_sphere.txt'
```

### Step 5: Call np.savetxt()

```python
np.savetxt(sphere_hsp_path, hsp_mm)
```

### Step 6: Assign hsp_dec = value

```python
hsp_dec = np.array([dig['r'] for dig in raw.info['dig']])[8:]
```

**Verification:**
```python
assert len(hsp_dec) > 5000
```

### Step 7: Assign dist = np.sqrt(...)

```python
dist = np.sqrt(np.sum((hsp_m - np.mean(hsp_m, axis=0)) ** 2, axis=1))
```

### Step 8: Assign dist_dec = np.sqrt(...)

```python
dist_dec = np.sqrt(np.sum((hsp_dec - np.mean(hsp_dec, axis=0)) ** 2, axis=1))
```

### Step 9: Assign hsp_rad = np.mean(...)

```python
hsp_rad = np.mean(dist)
```

### Step 10: Assign hsp_dec_rad = np.mean(...)

```python
hsp_dec_rad = np.mean(dist_dec)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hsp_rad, hsp_dec_rad, decimal=3)
```

### Step 12: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(sqd_path, mrk_path, elp_txt_path, sphere_hsp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test decimation of digitizer headshapes with too many points.'
hsp_mm = _get_ico_surface(5)['rr'] * 100
hsp_m = hsp_mm / 1000.0
sphere_hsp_path = tmp_path / 'test_sphere.txt'
np.savetxt(sphere_hsp_path, hsp_mm)
with pytest.warns(RuntimeWarning, match='was automatically downsampled .* FastScan'):
    raw = read_raw_kit(sqd_path, mrk_path, elp_txt_path, sphere_hsp_path)
hsp_dec = np.array([dig['r'] for dig in raw.info['dig']])[8:]
assert len(hsp_dec) > 5000
dist = np.sqrt(np.sum((hsp_m - np.mean(hsp_m, axis=0)) ** 2, axis=1))
dist_dec = np.sqrt(np.sum((hsp_dec - np.mean(hsp_dec, axis=0)) ** 2, axis=1))
hsp_rad = np.mean(dist)
hsp_dec_rad = np.mean(dist_dec)
assert_array_almost_equal(hsp_rad, hsp_dec_rad, decimal=3)
```

## Next Steps


---

*Source: test_kit.py:382 | Complexity: Advanced | Last updated: 2026-05-18*