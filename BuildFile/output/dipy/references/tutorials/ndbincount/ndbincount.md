# How To: Ndbincount

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ndbincount

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking._utils`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`
- `dipy.tracking.vox2track`


## Step-by-Step Guide

### Step 1: Assign x = value

```python
x = np.array([[0, 0], [0, 0], [0, 1], [0, 1], [1, 0], [2, 2]]).T
```

### Step 2: Assign expected = value

```python
expected = [2, 2, 1, 1]
```

### Step 3: Assign bc = ndbincount(...)

```python
bc = ndbincount(x)
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(bc.shape, (3, 3))
```

### Step 5: Call check()

```python
check(expected)
```

### Step 6: Assign bc = ndbincount(...)

```python
bc = ndbincount(x, shape=(4, 5))
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(bc.shape, (4, 5))
```

### Step 8: Call check()

```python
check(expected)
```

### Step 9: Assign weights = np.arange(...)

```python
weights = np.arange(6.0)
```

### Step 10: Assign unknown = 1.23

```python
weights[-1] = 1.23
```

### Step 11: Assign expected = value

```python
expected = [1.0, 5.0, 4.0, 1.23]
```

### Step 12: Assign bc = ndbincount(...)

```python
bc = ndbincount(x, weights=weights)
```

### Step 13: Call check()

```python
check(expected)
```

### Step 14: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, ndbincount, x, weights=None, shape=(2, 2))
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(bc[0, 0], expected[0])
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(bc[0, 1], expected[1])
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(bc[1, 0], expected[2])
```

### Step 18: Call npt.assert_equal()

```python
npt.assert_equal(bc[2, 2], expected[3])
```


## Complete Example

```python
# Workflow
def check(expected):
    npt.assert_equal(bc[0, 0], expected[0])
    npt.assert_equal(bc[0, 1], expected[1])
    npt.assert_equal(bc[1, 0], expected[2])
    npt.assert_equal(bc[2, 2], expected[3])
x = np.array([[0, 0], [0, 0], [0, 1], [0, 1], [1, 0], [2, 2]]).T
expected = [2, 2, 1, 1]
bc = ndbincount(x)
npt.assert_equal(bc.shape, (3, 3))
check(expected)
bc = ndbincount(x, shape=(4, 5))
npt.assert_equal(bc.shape, (4, 5))
check(expected)
weights = np.arange(6.0)
weights[-1] = 1.23
expected = [1.0, 5.0, 4.0, 1.23]
bc = ndbincount(x, weights=weights)
check(expected)
npt.assert_raises(ValueError, ndbincount, x, weights=None, shape=(2, 2))
```

## Next Steps


---

*Source: test_utils.py:317 | Complexity: Advanced | Last updated: 2026-05-18*