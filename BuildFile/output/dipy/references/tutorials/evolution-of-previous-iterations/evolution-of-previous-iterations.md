# How To: Evolution Of Previous Iterations

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test evolution of previous iterations

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
assert_equal(len(slm.matrix_history), slm.iterations)
```

### Step 2: Assign moving = value

```python
moving = fornix_streamlines()[:20]
```

### Step 3: Assign moving = value

```python
moving = [m + np.array([10.0, 0.0, 0.0]) for m in moving]
```

### Step 4: Assign slr = StreamlineLinearRegistration(...)

```python
slr = StreamlineLinearRegistration(evolution=True)
```

### Step 5: Assign slm = slr.optimize(...)

```python
slm = slr.optimize(static, moving)
```

### Step 6: Call assert_equal()

```python
assert_equal(len(slm.matrix_history), slm.iterations)
```


## Complete Example

```python
# Workflow
static = fornix_streamlines()[:20]
moving = fornix_streamlines()[:20]
moving = [m + np.array([10.0, 0.0, 0.0]) for m in moving]
slr = StreamlineLinearRegistration(evolution=True)
slm = slr.optimize(static, moving)
assert_equal(len(slm.matrix_history), slm.iterations)
```

## Next Steps


---

*Source: test_streamlinear.py:332 | Complexity: Intermediate | Last updated: 2026-05-18*