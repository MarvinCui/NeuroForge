# How To: Round Trip Spatialimages

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test round trip spatialimages

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileholders`
- `spatialimages`


## Step-by-Step Guide

### Step 1: Assign data = np.arange.reshape(...)

```python
data = np.arange(24, dtype='i4').reshape((2, 3, 4))
```

**Verification:**
```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 2: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

**Verification:**
```python
assert_array_equal(img3.get_fdata(), data)
```

### Step 3: Assign klasses = value

```python
klasses = [klass for klass in all_image_classes if klass.rw and klass.makeable and issubclass(klass, SpatialImage)]
```

### Step 4: Assign file_map = klass.make_file_map(...)

```python
file_map = klass.make_file_map()
```

### Step 5: Assign img = klass(...)

```python
img = klass(data, aff)
```

### Step 6: Assign img.file_map = file_map

```python
img.file_map = file_map
```

### Step 7: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 8: Assign img2 = klass.from_file_map(...)

```python
img2 = klass.from_file_map(file_map)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 10: Call img2.to_file_map()

```python
img2.to_file_map()
```

### Step 11: Assign img3 = klass.from_file_map(...)

```python
img3 = klass.from_file_map(file_map)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(img3.get_fdata(), data)
```

### Step 13: Assign unknown.fileobj = BytesIO(...)

```python
file_map[key].fileobj = BytesIO()
```


## Complete Example

```python
# Workflow
data = np.arange(24, dtype='i4').reshape((2, 3, 4))
aff = np.eye(4)
klasses = [klass for klass in all_image_classes if klass.rw and klass.makeable and issubclass(klass, SpatialImage)]
for klass in klasses:
    file_map = klass.make_file_map()
    for key in file_map:
        file_map[key].fileobj = BytesIO()
    img = klass(data, aff)
    img.file_map = file_map
    img.to_file_map()
    img2 = klass.from_file_map(file_map)
    assert_array_equal(img2.get_fdata(), data)
    img2.to_file_map()
    img3 = klass.from_file_map(file_map)
    assert_array_equal(img3.get_fdata(), data)
```

## Next Steps


---

*Source: test_files_interface.py:87 | Complexity: Advanced | Last updated: 2026-05-18*