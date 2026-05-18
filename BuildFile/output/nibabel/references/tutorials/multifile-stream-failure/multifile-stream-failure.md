# How To: Multifile Stream Failure

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multifile stream failure

## Prerequisites

**Required Modules:**
- `warnings`
- `itertools`
- `numpy`
- `pytest`
- `filebasedimages`
- `test_image_api`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 3, 4)
```

### Step 2: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(np.prod(shape), dtype=np.float32).reshape(shape)
```

### Step 3: Assign img = SerializableMPNumpyImage(...)

```python
img = SerializableMPNumpyImage(arr)
```

### Step 4: Assign img = SerializableNumpyImage(...)

```python
img = SerializableNumpyImage(arr)
```

### Step 5: Assign bstr = img.to_bytes(...)

```python
bstr = img.to_bytes()
```

### Step 6: Call img.to_bytes()

```python
img.to_bytes()
```

### Step 7: Call SerializableMPNumpyImage.from_bytes()

```python
SerializableMPNumpyImage.from_bytes(bstr)
```


## Complete Example

```python
# Workflow
shape = (2, 3, 4)
arr = np.arange(np.prod(shape), dtype=np.float32).reshape(shape)
img = SerializableMPNumpyImage(arr)
with pytest.raises(NotImplementedError):
    img.to_bytes()
img = SerializableNumpyImage(arr)
bstr = img.to_bytes()
with pytest.raises(NotImplementedError):
    SerializableMPNumpyImage.from_bytes(bstr)
```

## Next Steps


---

*Source: test_filebasedimages.py:135 | Complexity: Intermediate | Last updated: 2026-05-18*