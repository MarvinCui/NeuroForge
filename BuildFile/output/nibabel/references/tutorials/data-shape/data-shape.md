# How To: Data Shape

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test data shape

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
assert img.shape[:1] == (4,)
```

### Step 2: Assign arr = np.arange(...)

```python
arr = np.arange(4, dtype=np.int16)
```

**Verification:**
```python
assert np.prod(img.shape) == 4
```

### Step 3: Assign img = img_klass(...)

```python
img = img_klass(arr, np.eye(4))
```

**Verification:**
```python
assert img.shape == (2, 3, 4)
```

### Step 4: Assign img = img_klass(...)

```python
img = img_klass(np.zeros((2, 3, 4), dtype=np.float32), np.eye(4))
```

**Verification:**
```python
assert img.shape == (2, 3, 4)
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
arr = np.arange(4, dtype=np.int16)
img = img_klass(arr, np.eye(4))
assert img.shape[:1] == (4,)
assert np.prod(img.shape) == 4
img = img_klass(np.zeros((2, 3, 4), dtype=np.float32), np.eye(4))
assert img.shape == (2, 3, 4)
```

## Next Steps


---

*Source: test_spatialimages.py:275 | Complexity: Intermediate | Last updated: 2026-05-18*