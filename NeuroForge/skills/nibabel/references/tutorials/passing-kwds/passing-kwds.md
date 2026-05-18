# How To: Passing Kwds

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test passing kwds

## Prerequisites

**Required Modules:**
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.optpkg`
- `test_dicomwrappers`


## Step-by-Step Guide

### Step 1: Assign dwi_glob = 'siemens_dwi_*.dcm.gz'

```python
dwi_glob = 'siemens_dwi_*.dcm.gz'
```

**Verification:**
```python
assert_array_equal(data, data2)
```

### Step 2: Assign csa_glob = 'csa*.bin'

```python
csa_glob = 'csa*.bin'
```

### Step 3: Assign unknown = func(...)

```python
data, aff, bs, gs = func(IO_DATA_PATH, dwi_glob)
```

### Step 4: Assign unknown = func(...)

```python
data2, aff2, bs2, gs2 = func(IO_DATA_PATH, dwi_glob, dicom_kwargs=dict(force=True))
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(data, data2)
```

### Step 6: Call func()

```python
func(IO_DATA_PATH, dwi_glob, dicom_kwargs=dict(not_a_parameter=True))
```

### Step 7: Call func()

```python
func(IO_DATA_PATH, csa_glob)
```

### Step 8: Call func()

```python
func(IO_DATA_PATH, csa_glob, dicom_kwargs=dict(force=True))
```


## Complete Example

```python
# Workflow
dwi_glob = 'siemens_dwi_*.dcm.gz'
csa_glob = 'csa*.bin'
for func in (didr.read_mosaic_dwi_dir, didr.read_mosaic_dir):
    data, aff, bs, gs = func(IO_DATA_PATH, dwi_glob)
    data2, aff2, bs2, gs2 = func(IO_DATA_PATH, dwi_glob, dicom_kwargs=dict(force=True))
    assert_array_equal(data, data2)
    with pytest.raises(TypeError):
        func(IO_DATA_PATH, dwi_glob, dicom_kwargs=dict(not_a_parameter=True))
    with pytest.raises(pydicom.filereader.InvalidDicomError):
        func(IO_DATA_PATH, csa_glob)
    with pytest.raises(didr.DicomReadError):
        func(IO_DATA_PATH, csa_glob, dicom_kwargs=dict(force=True))
```

## Next Steps


---

*Source: test_dicomreaders.py:34 | Complexity: Advanced | Last updated: 2026-05-18*