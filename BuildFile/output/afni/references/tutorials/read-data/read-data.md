# How To: Read Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test read data

## Prerequisites

**Required Modules:**
- `py3k`
- `numpy`
- `spatialimages`
- `unittest`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign hdr = Header(...)

```python
hdr = Header(np.int32, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
```

**Verification:**
```python
assert_equal(fobj.getvalue(), data.astype(np.int32).tostring(order='F'))
```

### Step 2: Assign fobj = BytesIO(...)

```python
fobj = BytesIO()
```

**Verification:**
```python
assert_array_equal(data, data2)
```

### Step 3: Assign data = np.arange.reshape(...)

```python
data = np.arange(6).reshape((1, 2, 3))
```

### Step 4: Call hdr.data_to_fileobj()

```python
hdr.data_to_fileobj(data, fobj)
```

### Step 5: Call assert_equal()

```python
assert_equal(fobj.getvalue(), data.astype(np.int32).tostring(order='F'))
```

### Step 6: Call fobj.seek()

```python
fobj.seek(0)
```

### Step 7: Assign data2 = hdr.data_from_fileobj(...)

```python
data2 = hdr.data_from_fileobj(fobj)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(data, data2)
```


## Complete Example

```python
# Workflow
hdr = Header(np.int32, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
fobj = BytesIO()
data = np.arange(6).reshape((1, 2, 3))
hdr.data_to_fileobj(data, fobj)
assert_equal(fobj.getvalue(), data.astype(np.int32).tostring(order='F'))
fobj.seek(0)
data2 = hdr.data_from_fileobj(fobj)
assert_array_equal(data, data2)
```

## Next Steps


---

*Source: test_spatialimages.py:157 | Complexity: Advanced | Last updated: 2026-05-18*