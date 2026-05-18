# How To: Files Spatialimages

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test files spatialimages

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileholders`
- `spatialimages`


## Step-by-Step Guide

### Step 1: Assign arr = np.zeros(...)

```python
arr = np.zeros((2, 3, 4))
```

**Verification:**
```python
assert value.filename is None
```

### Step 2: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

**Verification:**
```python
assert value.fileobj is None
```

### Step 3: Assign klasses = value

```python
klasses = [klass for klass in all_image_classes if klass.rw and issubclass(klass, SpatialImage)]
```

**Verification:**
```python
assert value.pos == 0
```

### Step 4: Assign file_map = klass.make_file_map(...)

```python
file_map = klass.make_file_map()
```

**Verification:**
```python
assert value.filename is None
```

### Step 5: Assign img = klass(...)

```python
img = klass(arr.astype(np.float32), aff)
```

**Verification:**
```python
assert value.fileobj is None
```

### Step 6: Assign img = klass(...)

```python
img = klass(arr, aff)
```

**Verification:**
```python
assert value.pos == 0
```


## Complete Example

```python
# Workflow
arr = np.zeros((2, 3, 4))
aff = np.eye(4)
klasses = [klass for klass in all_image_classes if klass.rw and issubclass(klass, SpatialImage)]
for klass in klasses:
    file_map = klass.make_file_map()
    for value in file_map.values():
        assert value.filename is None
        assert value.fileobj is None
        assert value.pos == 0
    if not klass.makeable:
        continue
    if klass == MGHImage:
        img = klass(arr.astype(np.float32), aff)
    else:
        img = klass(arr, aff)
    for value in img.file_map.values():
        assert value.filename is None
        assert value.fileobj is None
        assert value.pos == 0
```

## Next Steps


---

*Source: test_files_interface.py:22 | Complexity: Intermediate | Last updated: 2026-05-18*