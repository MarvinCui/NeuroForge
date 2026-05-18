# How To: Stream Rigid

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test stream rigid

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.bundlemin`
- `dipy.align.streamlinear`
- `dipy.core.geometry`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign static = value

```python
static = fornix_streamlines()[:20]
```

**Verification:**
```python
assert_array_almost_equal(moved[0], moved2[0], decimal=3)
```

### Step 2: Assign moving = value

```python
moving = fornix_streamlines()[20:40]
```

**Verification:**
```python
assert_array_almost_equal(moved2[0], moved3[0], decimal=3)
```

### Step 3: Call center_streamlines()

```python
center_streamlines(static)
```

### Step 4: Assign mat = compose_matrix44(...)

```python
mat = compose_matrix44([0, 0, 0, 0, 40, 0])
```

### Step 5: Assign moving = transform_streamlines(...)

```python
moving = transform_streamlines(moving, mat)
```

### Step 6: Assign srr = StreamlineLinearRegistration(...)

```python
srr = StreamlineLinearRegistration()
```

### Step 7: Assign sr_params = srr.optimize(...)

```python
sr_params = srr.optimize(static, moving)
```

### Step 8: Assign moved = transform_streamlines(...)

```python
moved = transform_streamlines(moving, sr_params.matrix)
```

### Step 9: Assign srr = StreamlineLinearRegistration(...)

```python
srr = StreamlineLinearRegistration(verbose=True)
```

### Step 10: Assign srm = srr.optimize(...)

```python
srm = srr.optimize(static, moving)
```

### Step 11: Assign moved2 = transform_streamlines(...)

```python
moved2 = transform_streamlines(moving, srm.matrix)
```

### Step 12: Assign moved3 = srm.transform(...)

```python
moved3 = srm.transform(moving)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(moved[0], moved2[0], decimal=3)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(moved2[0], moved3[0], decimal=3)
```


## Complete Example

```python
# Workflow
static = fornix_streamlines()[:20]
moving = fornix_streamlines()[20:40]
center_streamlines(static)
mat = compose_matrix44([0, 0, 0, 0, 40, 0])
moving = transform_streamlines(moving, mat)
srr = StreamlineLinearRegistration()
sr_params = srr.optimize(static, moving)
moved = transform_streamlines(moving, sr_params.matrix)
srr = StreamlineLinearRegistration(verbose=True)
srm = srr.optimize(static, moving)
moved2 = transform_streamlines(moving, srm.matrix)
moved3 = srm.transform(moving)
assert_array_almost_equal(moved[0], moved2[0], decimal=3)
assert_array_almost_equal(moved2[0], moved3[0], decimal=3)
```

## Next Steps


---

*Source: test_streamlinear.py:165 | Complexity: Advanced | Last updated: 2026-05-18*