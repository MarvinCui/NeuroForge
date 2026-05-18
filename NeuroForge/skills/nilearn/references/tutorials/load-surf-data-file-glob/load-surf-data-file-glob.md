# How To: Load Surf Data File Glob

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load surf data file glob

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

### Step 1: Assign data2D = np.ones(...)

```python
data2D = np.ones((20, 3))
```

**Verification:**
```python
assert_array_equal(load_surf_data(tmp_path / 'glob*.gii'), data2D)
```

### Step 2: Assign fnames = value

```python
fnames = []
```

**Verification:**
```python
assert_array_equal(load_surf_data(tmp_path / 'glob*.gii'), data2D)
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(load_surf_data(tmp_path / 'glob*.gii'), data2D)
```

### Step 4: Assign filename = value

```python
filename = tmp_path / 'glob_3_tmp.gii'
```

### Step 5: Call fnames.append()

```python
fnames.append(filename)
```

### Step 6: Assign darray1 = gifti.GiftiDataArray(...)

```python
darray1 = gifti.GiftiDataArray(data=np.ones((20,)), datatype='NIFTI_TYPE_FLOAT32')
```

### Step 7: Assign gii = gifti.GiftiImage(...)

```python
gii = gifti.GiftiImage(darrays=[darray1, darray1, darray1])
```

### Step 8: Call gii.to_filename()

```python
gii.to_filename(fnames[-1])
```

### Step 9: Assign data2D = np.concatenate(...)

```python
data2D = np.concatenate((data2D, np.ones((20, 3))), axis=1)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(load_surf_data(tmp_path / 'glob*.gii'), data2D)
```

### Step 11: Assign filename = value

```python
filename = tmp_path / 'glob_4_tmp.gii'
```

### Step 12: Call fnames.append()

```python
fnames.append(filename)
```

### Step 13: Assign darray = gifti.GiftiDataArray(...)

```python
darray = gifti.GiftiDataArray(data=np.ones((15, 1)), datatype='NIFTI_TYPE_FLOAT32')
```

### Step 14: Assign gii = gifti.GiftiImage(...)

```python
gii = gifti.GiftiImage(darrays=[darray])
```

### Step 15: Call gii.to_filename()

```python
gii.to_filename(fnames[-1])
```

### Step 16: Assign filename = value

```python
filename = tmp_path / f'glob_{f}_tmp.gii'
```

### Step 17: Call fnames.append()

```python
fnames.append(filename)
```

### Step 18: Assign darray = gifti.GiftiDataArray(...)

```python
darray = gifti.GiftiDataArray(data=data2D[:, f], datatype='NIFTI_TYPE_FLOAT32')
```

### Step 19: Assign gii = gifti.GiftiImage(...)

```python
gii = gifti.GiftiImage(darrays=[darray])
```

### Step 20: Call gii.to_filename()

```python
gii.to_filename(fnames[f])
```

### Step 21: Call load_surf_data()

```python
load_surf_data(tmp_path / '*.gii')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
data2D = np.ones((20, 3))
fnames = []
for f in range(3):
    filename = tmp_path / f'glob_{f}_tmp.gii'
    fnames.append(filename)
    data2D[:, f] *= f
    darray = gifti.GiftiDataArray(data=data2D[:, f], datatype='NIFTI_TYPE_FLOAT32')
    gii = gifti.GiftiImage(darrays=[darray])
    gii.to_filename(fnames[f])
assert_array_equal(load_surf_data(tmp_path / 'glob*.gii'), data2D)
filename = tmp_path / 'glob_3_tmp.gii'
fnames.append(filename)
darray1 = gifti.GiftiDataArray(data=np.ones((20,)), datatype='NIFTI_TYPE_FLOAT32')
gii = gifti.GiftiImage(darrays=[darray1, darray1, darray1])
gii.to_filename(fnames[-1])
data2D = np.concatenate((data2D, np.ones((20, 3))), axis=1)
assert_array_equal(load_surf_data(tmp_path / 'glob*.gii'), data2D)
filename = tmp_path / 'glob_4_tmp.gii'
fnames.append(filename)
darray = gifti.GiftiDataArray(data=np.ones((15, 1)), datatype='NIFTI_TYPE_FLOAT32')
gii = gifti.GiftiImage(darrays=[darray])
gii.to_filename(fnames[-1])
with pytest.raises(ValueError, match='files must contain data with the same shape'):
    load_surf_data(tmp_path / '*.gii')
```

## Next Steps


---

*Source: test_surface.py:397 | Complexity: Advanced | Last updated: 2026-05-18*