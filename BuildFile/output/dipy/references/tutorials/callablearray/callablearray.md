# How To: Callablearray

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test CallableArray

## Prerequisites

**Required Modules:**
- `functools`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.reconst.multi_voxel`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign callarray = CallableArray(...)

```python
callarray = CallableArray((2, 3), dtype=object)
```

### Step 2: Assign unknown = value

```python
callarray[:] = np.arange
```

### Step 3: Assign expected = np.empty(...)

```python
expected = np.empty([2, 3, 4])
```

### Step 4: Assign unknown = range(...)

```python
expected[:] = range(4)
```

### Step 5: Call npt.assert_array_equal()

```python
npt.assert_array_equal(callarray(4), expected)
```

### Step 6: Assign unknown = None

```python
callarray[0, 0] = None
```

### Step 7: Assign unknown = 0

```python
expected[0, 0] = 0
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(callarray(4), expected)
```


## Complete Example

```python
# Workflow
callarray = CallableArray((2, 3), dtype=object)
callarray[:] = np.arange
expected = np.empty([2, 3, 4])
expected[:] = range(4)
npt.assert_array_equal(callarray(4), expected)
callarray[0, 0] = None
expected[0, 0] = 0
npt.assert_array_equal(callarray(4), expected)
```

## Next Steps


---

*Source: test_multi_voxel.py:128 | Complexity: Advanced | Last updated: 2026-05-18*