# How To: Sphharmfit

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test SphHarmFit

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.interpolation`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign coef = np.zeros(...)

```python
coef = np.zeros((3, 4, 5, 45))
```

**Verification:**
```python
assert_equal(item.shape, ())
```

### Step 2: Assign mask = np.zeros(...)

```python
mask = np.zeros((3, 4, 5), dtype=bool)
```

**Verification:**
```python
assert_equal(data.shape, (4, 5))
```

### Step 3: Assign fit = SphHarmFit(...)

```python
fit = SphHarmFit(None, coef, mask)
```

**Verification:**
```python
assert_equal(data.shape, (3, 4))
```

### Step 4: Assign item = value

```python
item = fit[0, 0, 0]
```

### Step 5: Call assert_equal()

```python
assert_equal(item.shape, ())
```

### Step 6: Assign data = value

```python
data = fit[0]
```

### Step 7: Call assert_equal()

```python
assert_equal(data.shape, (4, 5))
```

### Step 8: Assign data = value

```python
data = fit[:, :, 0]
```

### Step 9: Call assert_equal()

```python
assert_equal(data.shape, (3, 4))
```


## Complete Example

```python
# Workflow
coef = np.zeros((3, 4, 5, 45))
mask = np.zeros((3, 4, 5), dtype=bool)
fit = SphHarmFit(None, coef, mask)
item = fit[0, 0, 0]
assert_equal(item.shape, ())
data = fit[0]
assert_equal(data.shape, (4, 5))
data = fit[:, :, 0]
assert_equal(data.shape, (3, 4))
```

## Next Steps


---

*Source: test_shm.py:661 | Complexity: Advanced | Last updated: 2026-05-18*