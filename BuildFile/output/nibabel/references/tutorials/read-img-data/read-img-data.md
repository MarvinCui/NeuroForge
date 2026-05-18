# How To: Read Img Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read img data

## Prerequisites

**Required Modules:**
- `pathlib`
- `shutil`
- `os.path`
- `os.path`
- `tempfile`
- `numpy`
- `_compression`
- `filebasedimages`
- `loadsave`
- `openers`
- `optpkg`
- `testing`
- `tmpdirs`
- `pytest`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign fnames_test = value

```python
fnames_test = ['example4d.nii.gz', 'example_nifti2.nii.gz', 'minc1_1_scale.mnc', 'minc1_4d.mnc', 'test.mgz', 'tiny.mnc']
```

**Verification:**
```python
assert_array_equal(data, data2)
```

### Step 2: Assign fpath = pjoin(...)

```python
fpath = pjoin(data_path, fname)
```

**Verification:**
```python
assert (dao.slope, dao.inter) == (1, 0)
```

### Step 3: Assign img = load(...)

```python
img = load(fpath)
```

**Verification:**
```python
assert_array_equal(read_img_data(img, prefer='unscaled'), data)
```

### Step 4: Assign data = img.get_fdata(...)

```python
data = img.get_fdata()
```

**Verification:**
```python
assert_array_equal(img.dataobj, data)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(data, data2)
```

### Step 6: Assign dao = value

```python
dao = img.dataobj
```

### Step 7: Assign fpath = pathlib.Path(...)

```python
fpath = pathlib.Path(fpath)
```

### Step 8: Assign data2 = read_img_data(...)

```python
data2 = read_img_data(img)
```

**Verification:**
```python
assert (dao.slope, dao.inter) == (1, 0)
```

### Step 9: Assign up_fpath = pjoin(...)

```python
up_fpath = pjoin(tmpdir, str(fname).upper())
```

### Step 10: Call shutil.copyfile()

```python
shutil.copyfile(fpath, up_fpath)
```

### Step 11: Assign img = load(...)

```python
img = load(up_fpath)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(img.dataobj, data)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(read_img_data(img, prefer='unscaled'), data)
```

### Step 14: Assign up_fpath = pathlib.Path(...)

```python
up_fpath = pathlib.Path(up_fpath)
```


## Complete Example

```python
# Workflow
fnames_test = ['example4d.nii.gz', 'example_nifti2.nii.gz', 'minc1_1_scale.mnc', 'minc1_4d.mnc', 'test.mgz', 'tiny.mnc']
fnames_test += [pathlib.Path(p) for p in fnames_test]
for fname in fnames_test:
    fpath = pjoin(data_path, fname)
    if isinstance(fname, pathlib.Path):
        fpath = pathlib.Path(fpath)
    img = load(fpath)
    data = img.get_fdata()
    with deprecated_to('5.0.0'):
        data2 = read_img_data(img)
    assert_array_equal(data, data2)
    dao = img.dataobj
    if hasattr(dao, 'slope') and hasattr(img.header, 'raw_data_from_fileobj'):
        assert (dao.slope, dao.inter) == (1, 0)
        with deprecated_to('5.0.0'):
            assert_array_equal(read_img_data(img, prefer='unscaled'), data)
    with TemporaryDirectory() as tmpdir:
        up_fpath = pjoin(tmpdir, str(fname).upper())
        if isinstance(fname, pathlib.Path):
            up_fpath = pathlib.Path(up_fpath)
        shutil.copyfile(fpath, up_fpath)
        img = load(up_fpath)
        assert_array_equal(img.dataobj, data)
        del img
```

## Next Steps


---

*Source: test_loadsave.py:36 | Complexity: Advanced | Last updated: 2026-05-18*