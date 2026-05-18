# How To: Read Img Arr Or Path

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read img arr or path

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `tempfile`
- `urllib.error`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `trx.trx_file_memmap`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.io.surface`
- `dipy.io.utils`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign data = rng.random(...)

```python
data = rng.random((4, 4, 4, 3))
```

**Verification:**
```python
assert np.allclose(dd, data)
```

### Step 2: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

**Verification:**
```python
assert np.allclose(aa, aff)
```

### Step 3: Assign unknown = rng.standard_normal(...)

```python
aff[:3, :] = rng.standard_normal((3, 4))
```

**Verification:**
```python
assert np.allclose(dd, data)
```

### Step 4: Assign img = nib.Nifti1Image(...)

```python
img = nib.Nifti1Image(data, aff)
```

**Verification:**
```python
assert np.allclose(aa, aff)
```

### Step 5: Assign path = value

```python
path = tempfile.NamedTemporaryFile().name + '.nii.gz'
```

### Step 6: Call nib.save()

```python
nib.save(img, path)
```

### Step 7: Assign unknown = read_img_arr_or_path(...)

```python
dd, aa = read_img_arr_or_path(path)
```

**Verification:**
```python
assert np.allclose(dd, data)
```

### Step 8: Assign unknown = read_img_arr_or_path(...)

```python
dd, aa = read_img_arr_or_path(this, affine=aff)
```

**Verification:**
```python
assert np.allclose(dd, data)
```

### Step 9: Call read_img_arr_or_path()

```python
read_img_arr_or_path(data)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
data = rng.random((4, 4, 4, 3))
aff = np.eye(4)
aff[:3, :] = rng.standard_normal((3, 4))
img = nib.Nifti1Image(data, aff)
path = tempfile.NamedTemporaryFile().name + '.nii.gz'
nib.save(img, path)
for this in [data, img, path]:
    dd, aa = read_img_arr_or_path(this, affine=aff)
    assert np.allclose(dd, data)
    assert np.allclose(aa, aff)
with pytest.raises(ValueError):
    read_img_arr_or_path(data)
dd, aa = read_img_arr_or_path(path)
assert np.allclose(dd, data)
assert np.allclose(aa, aff)
```

## Next Steps


---

*Source: test_utils.py:243 | Complexity: Advanced | Last updated: 2026-05-18*