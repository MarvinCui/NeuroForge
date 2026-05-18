# How To: Load Surf Data File Freesurfer

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load surf data file freesurfer

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy.spatial`
- `scipy.stats`
- `sklearn.exceptions`
- `nilearn`
- `nilearn._utils`
- `nilearn._utils.helpers`
- `nilearn.image`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign filename_area = value

```python
filename_area = tmp_path / 'tmp.area'
```

**Verification:**
```python
assert_array_equal(load_surf_data(filename_area), np.zeros((20,)))
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((20,))
```

**Verification:**
```python
assert_array_equal(load_surf_data(filename_curv), np.zeros((20,)))
```

### Step 3: Call freesurfer.io.write_morph_data()

```python
freesurfer.io.write_morph_data(filename_area, data)
```

**Verification:**
```python
assert_array_equal(load_surf_data(filename_sulc), np.zeros((20,)))
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(load_surf_data(filename_area), np.zeros((20,)))
```

**Verification:**
```python
assert_array_equal(load_surf_data(filename_thick), np.zeros((20,)))
```

### Step 5: Assign filename_curv = value

```python
filename_curv = tmp_path / 'tmp.curv'
```

**Verification:**
```python
assert_array_equal(label[:5], label_start)
```

### Step 6: Call freesurfer.io.write_morph_data()

```python
freesurfer.io.write_morph_data(filename_curv, data)
```

**Verification:**
```python
assert_array_equal(label[-5:], label_end)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(load_surf_data(filename_curv), np.zeros((20,)))
```

**Verification:**
```python
assert label.shape == (10,)
```

### Step 8: Assign filename_sulc = value

```python
filename_sulc = tmp_path / 'tmp.sulc'
```

**Verification:**
```python
assert_array_equal(annot[:10], annot_start)
```

### Step 9: Call freesurfer.io.write_morph_data()

```python
freesurfer.io.write_morph_data(filename_sulc, data)
```

**Verification:**
```python
assert_array_equal(annot[-10:], annot_end)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(load_surf_data(filename_sulc), np.zeros((20,)))
```

**Verification:**
```python
assert annot.shape == (10242,)
```

### Step 11: Assign filename_thick = value

```python
filename_thick = tmp_path / 'tmp.thickness'
```

### Step 12: Call freesurfer.io.write_morph_data()

```python
freesurfer.io.write_morph_data(filename_thick, data)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(load_surf_data(filename_thick), np.zeros((20,)))
```

### Step 14: Assign label_start = np.array(...)

```python
label_start = np.array([5900, 5899, 5901, 5902, 2638])
```

### Step 15: Assign label_end = np.array(...)

```python
label_end = np.array([8756, 6241, 8757, 1896, 6243])
```

### Step 16: Assign label = load_surf_data(...)

```python
label = load_surf_data(datadir / 'test.label')
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(label[:5], label_start)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(label[-5:], label_end)
```

**Verification:**
```python
assert label.shape == (10,)
```

### Step 19: Assign annot_start = np.array(...)

```python
annot_start = np.array([24, 29, 28, 27, 24, 31, 11, 25, 0, 12])
```

### Step 20: Assign annot_end = np.array(...)

```python
annot_end = np.array([16, 16, 16, 16, 16, 16, 16, 16, 16, 16])
```

### Step 21: Assign annot = load_surf_data(...)

```python
annot = load_surf_data(datadir / 'test.annot')
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(annot[:10], annot_start)
```

### Step 23: Call assert_array_equal()

```python
assert_array_equal(annot[-10:], annot_end)
```

**Verification:**
```python
assert annot.shape == (10242,)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
filename_area = tmp_path / 'tmp.area'
data = np.zeros((20,))
freesurfer.io.write_morph_data(filename_area, data)
assert_array_equal(load_surf_data(filename_area), np.zeros((20,)))
filename_curv = tmp_path / 'tmp.curv'
freesurfer.io.write_morph_data(filename_curv, data)
assert_array_equal(load_surf_data(filename_curv), np.zeros((20,)))
filename_sulc = tmp_path / 'tmp.sulc'
freesurfer.io.write_morph_data(filename_sulc, data)
assert_array_equal(load_surf_data(filename_sulc), np.zeros((20,)))
filename_thick = tmp_path / 'tmp.thickness'
freesurfer.io.write_morph_data(filename_thick, data)
assert_array_equal(load_surf_data(filename_thick), np.zeros((20,)))
label_start = np.array([5900, 5899, 5901, 5902, 2638])
label_end = np.array([8756, 6241, 8757, 1896, 6243])
label = load_surf_data(datadir / 'test.label')
assert_array_equal(label[:5], label_start)
assert_array_equal(label[-5:], label_end)
assert label.shape == (10,)
del label, label_start, label_end
annot_start = np.array([24, 29, 28, 27, 24, 31, 11, 25, 0, 12])
annot_end = np.array([16, 16, 16, 16, 16, 16, 16, 16, 16, 16])
annot = load_surf_data(datadir / 'test.annot')
assert_array_equal(annot[:10], annot_start)
assert_array_equal(annot[-10:], annot_end)
assert annot.shape == (10242,)
del annot, annot_start, annot_end
```

## Next Steps


---

*Source: test_surface.py:177 | Complexity: Advanced | Last updated: 2026-05-18*