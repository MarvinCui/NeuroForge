# How To: Fast Cross 3D

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test cross product with lots of elements.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test cross product with lots of elements.'

```python
'Test cross product with lots of elements.'
```

**Verification:**
```python
assert_array_equal(z, zz)
```

### Step 2: Assign x = rng.rand(...)

```python
x = rng.rand(100000, 3)
```

**Verification:**
```python
assert_array_equal(z, zz[:, 0])
```

### Step 3: Assign y = rng.rand(...)

```python
y = rng.rand(1, 3)
```

### Step 4: Assign z = np.cross(...)

```python
z = np.cross(x, y)
```

### Step 5: Assign zz = fast_cross_3d(...)

```python
zz = fast_cross_3d(x, y)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(z, zz)
```

### Step 7: Assign zz = fast_cross_3d(...)

```python
zz = fast_cross_3d(x[:, np.newaxis], y[0])
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(z, zz[:, 0])
```


## Complete Example

```python
# Workflow
'Test cross product with lots of elements.'
x = rng.rand(100000, 3)
y = rng.rand(1, 3)
z = np.cross(x, y)
zz = fast_cross_3d(x, y)
assert_array_equal(z, zz)
zz = fast_cross_3d(x[:, np.newaxis], y[0])
assert_array_equal(z, zz[:, 0])
```

## Next Steps


---

*Source: test_surface.py:88 | Complexity: Advanced | Last updated: 2026-05-18*