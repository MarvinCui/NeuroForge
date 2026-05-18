# How To: Get Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get data

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `imageclasses`
- `spatialimages`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign img_klass = value

```python
img_klass = self.image_class
```

**Verification:**
```python
assert in_data is img.dataobj
```

### Step 2: Assign in_data_template = np.arange.reshape(...)

```python
in_data_template = np.arange(24, dtype=np.int16).reshape((2, 3, 4))
```

**Verification:**
```python
assert in_data is out_data
```

### Step 3: Assign in_data = in_data_template.copy(...)

```python
in_data = in_data_template.copy()
```

**Verification:**
```python
assert in_data is out_data
```

### Step 4: Assign img = img_klass(...)

```python
img = img_klass(in_data, None)
```

**Verification:**
```python
assert (out_data == in_data_template).all()
```

### Step 5: Call img.uncache()

```python
img.uncache()
```

**Verification:**
```python
assert in_data is not rt_img.dataobj
```

### Step 6: Assign rt_img = bytesio_round_trip(...)

```python
rt_img = bytesio_round_trip(img)
```

**Verification:**
```python
assert (rt_img.dataobj == in_data).all()
```

### Step 7: Assign unknown = 42

```python
out_data[:] = 42
```

**Verification:**
```python
assert (out_data == in_data).all()
```

### Step 8: Call rt_img.uncache()

```python
rt_img.uncache()
```

**Verification:**
```python
assert rt_img.dataobj is not out_data
```

### Step 9: Assign out_data = img.get_data(...)

```python
out_data = img.get_data()
```

**Verification:**
```python
assert rt_img.get_data() is out_data
```

### Step 10: Assign out_data = rt_img.get_data(...)

```python
out_data = rt_img.get_data()
```

**Verification:**
```python
assert rt_img.get_data() is not out_data
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
in_data_template = np.arange(24, dtype=np.int16).reshape((2, 3, 4))
in_data = in_data_template.copy()
img = img_klass(in_data, None)
assert in_data is img.dataobj
with deprecated_to('5.0.0'):
    out_data = img.get_data()
assert in_data is out_data
img.uncache()
assert in_data is out_data
assert (out_data == in_data_template).all()
if not self.can_save:
    return
rt_img = bytesio_round_trip(img)
assert in_data is not rt_img.dataobj
assert (rt_img.dataobj == in_data).all()
with deprecated_to('5.0.0'):
    out_data = rt_img.get_data()
assert (out_data == in_data).all()
assert rt_img.dataobj is not out_data
with deprecated_to('5.0.0'):
    assert rt_img.get_data() is out_data
out_data[:] = 42
rt_img.uncache()
with deprecated_to('5.0.0'):
    assert rt_img.get_data() is not out_data
with deprecated_to('5.0.0'):
    assert (rt_img.get_data() == in_data).all()
```

## Next Steps


---

*Source: test_spatialimages.py:363 | Complexity: Advanced | Last updated: 2026-05-18*