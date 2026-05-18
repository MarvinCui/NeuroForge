# How To: Wrapper Args Kwds

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test wrapper args kwds

## Prerequisites

**Required Modules:**
- `gzip`
- `copy`
- `decimal`
- `hashlib`
- `os.path`
- `os.path`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `openers`
- `tests.nibabel_data`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign dcm = didw.wrapper_from_file(...)

```python
dcm = didw.wrapper_from_file(DATA_FILE)
```

**Verification:**
```python
assert_array_equal(data, dcm2.get_data())
```

### Step 2: Assign data = dcm.get_data(...)

```python
data = dcm.get_data()
```

**Verification:**
```python
assert_array_equal(data, dcm2.get_data())
```

### Step 3: Assign dcm2 = didw.wrapper_from_file(...)

```python
dcm2 = didw.wrapper_from_file(DATA_FILE, np.inf)
```

**Verification:**
```python
assert not dcm_malo.is_mosaic
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(data, dcm2.get_data())
```

### Step 5: Assign dcm2 = didw.wrapper_from_file(...)

```python
dcm2 = didw.wrapper_from_file(DATA_FILE, defer_size=np.inf)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(data, dcm2.get_data())
```

### Step 7: Assign csa_fname = pjoin(...)

```python
csa_fname = pjoin(IO_DATA_PATH, 'csa2_b0.bin')
```

### Step 8: Assign dcm_malo = didw.wrapper_from_file(...)

```python
dcm_malo = didw.wrapper_from_file(csa_fname, force=True)
```

**Verification:**
```python
assert not dcm_malo.is_mosaic
```

### Step 9: Call didw.wrapper_from_file()

```python
didw.wrapper_from_file(csa_fname)
```


## Complete Example

```python
# Workflow
dcm = didw.wrapper_from_file(DATA_FILE)
data = dcm.get_data()
dcm2 = didw.wrapper_from_file(DATA_FILE, np.inf)
assert_array_equal(data, dcm2.get_data())
dcm2 = didw.wrapper_from_file(DATA_FILE, defer_size=np.inf)
assert_array_equal(data, dcm2.get_data())
csa_fname = pjoin(IO_DATA_PATH, 'csa2_b0.bin')
with pytest.raises(pydicom.filereader.InvalidDicomError):
    didw.wrapper_from_file(csa_fname)
dcm_malo = didw.wrapper_from_file(csa_fname, force=True)
assert not dcm_malo.is_mosaic
```

## Next Steps


---

*Source: test_dicomwrappers.py:182 | Complexity: Advanced | Last updated: 2026-05-18*