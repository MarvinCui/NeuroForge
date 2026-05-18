# How To: Apply

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test apply

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `affines`
- `nifti1`
- `orientations`
- `testing`


## Step-by-Step Guide

### Step 1: Assign a = np.arange.reshape(...)

```python
a = np.arange(24).reshape((2, 3, 4))
```

**Verification:**
```python
assert t_arr.ndim == 4
```

### Step 2: Assign ornt = value

```python
ornt = OUT_ORNTS[-1]
```

**Verification:**
```python
assert_array_equal(a.shape, np.array(t_arr.shape)[np.array(ornt)[:, 0]])
```

### Step 3: Assign t_arr = apply_orientation(...)

```python
t_arr = apply_orientation(a[:, :, :, None], ornt)
```

**Verification:**
```python
assert t_arr.ndim == 4
```

### Step 4: Call apply_orientation()

```python
apply_orientation(a[:, :, 1], ornt)
```

### Step 5: Call apply_orientation()

```python
apply_orientation(a, [[0, 1], [np.nan, np.nan], [2, 1]])
```

### Step 6: Assign t_arr = apply_orientation(...)

```python
t_arr = apply_orientation(a, ornt)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(a.shape, np.array(t_arr.shape)[np.array(ornt)[:, 0]])
```


## Complete Example

```python
# Workflow
a = np.arange(24).reshape((2, 3, 4))
ornt = OUT_ORNTS[-1]
t_arr = apply_orientation(a[:, :, :, None], ornt)
assert t_arr.ndim == 4
with pytest.raises(OrientationError):
    apply_orientation(a[:, :, 1], ornt)
with pytest.raises(OrientationError):
    apply_orientation(a, [[0, 1], [np.nan, np.nan], [2, 1]])
for ornt in ALL_ORNTS:
    t_arr = apply_orientation(a, ornt)
    assert_array_equal(a.shape, np.array(t_arr.shape)[np.array(ornt)[:, 0]])
```

## Next Steps


---

*Source: test_orientations.py:174 | Complexity: Intermediate | Last updated: 2026-05-18*