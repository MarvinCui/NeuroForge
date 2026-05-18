# How To: Edge Nan

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test edge nan

## Prerequisites

**Required Modules:**
- `numpy`
- `nilearn.plotting.displays.edge_detect`


## Step-by-Step Guide

### Step 1: Assign img = np.zeros(...)

```python
img = np.zeros((10, 10))
```

**Verification:**
```python
assert (grad_mag[0] > 2).all()
```

### Step 2: Assign unknown = 1

```python
img[:5] = 1
```

### Step 3: Assign unknown = value

```python
img[0] = np.nan
```

### Step 4: Assign unknown = _edge_detect(...)

```python
grad_mag, _ = _edge_detect(img)
```

### Step 5: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(img[4], 1)
```

**Verification:**
```python
assert (grad_mag[0] > 2).all()
```


## Complete Example

```python
# Workflow
img = np.zeros((10, 10))
img[:5] = 1
img[0] = np.nan
grad_mag, _ = _edge_detect(img)
np.testing.assert_almost_equal(img[4], 1)
assert (grad_mag[0] > 2).all()
```

## Next Steps


---

*Source: test_edge_detect.py:13 | Complexity: Intermediate | Last updated: 2026-05-18*