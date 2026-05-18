# How To: Predict Shape

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test predict shape

## Prerequisites

**Required Modules:**
- `time`
- `functools`
- `io`
- `itertools`
- `threading`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileslice`


## Step-by-Step Guide

### Step 1: Assign shapes = value

```python
shapes = (15, 16, 17, 18)
```

**Verification:**
```python
assert predict_shape(sliceobj, shape) == arr[sliceobj].shape
```

### Step 2: Assign shape = value

```python
shape = shapes[:n_dim + 1]
```

**Verification:**
```python
assert predict_shape((Ellipsis,), (2, 3)) == (2, 3)
```

### Step 3: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(np.prod(shape)).reshape(shape)
```

**Verification:**
```python
assert predict_shape((Ellipsis, 1), (2, 3)) == (2,)
```

### Step 4: Assign slicers_list = value

```python
slicers_list = []
```

**Verification:**
```python
assert predict_shape((1, Ellipsis), (2, 3)) == (3,)
```

### Step 5: Call slicers_list.append()

```python
slicers_list.append(_slices_for_len(shape[i]))
```

**Verification:**
```python
assert predict_shape((1, slice(None), Ellipsis), (2, 3)) == (3,)
```


## Complete Example

```python
# Workflow
shapes = (15, 16, 17, 18)
for n_dim in range(len(shapes)):
    shape = shapes[:n_dim + 1]
    arr = np.arange(np.prod(shape)).reshape(shape)
    slicers_list = []
    for i in range(n_dim):
        slicers_list.append(_slices_for_len(shape[i]))
        for sliceobj in product(*slicers_list):
            assert predict_shape(sliceobj, shape) == arr[sliceobj].shape
assert predict_shape((Ellipsis,), (2, 3)) == (2, 3)
assert predict_shape((Ellipsis, 1), (2, 3)) == (2,)
assert predict_shape((1, Ellipsis), (2, 3)) == (3,)
assert predict_shape((1, slice(None), Ellipsis), (2, 3)) == (3,)
assert predict_shape((None,), (2, 3)) == (1, 2, 3)
assert predict_shape((None, 1), (2, 3)) == (1, 3)
assert predict_shape((1, None, slice(None)), (2, 3)) == (1, 3)
assert predict_shape((1, slice(None), None), (2, 3)) == (3, 1)
```

## Next Steps


---

*Source: test_fileslice.py:589 | Complexity: Intermediate | Last updated: 2026-05-18*