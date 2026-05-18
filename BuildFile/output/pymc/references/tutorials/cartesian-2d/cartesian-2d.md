# How To: Cartesian 2D

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cartesian 2d

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc.math`
- `pymc.pytensorf`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(1)
```

### Step 2: Assign a = value

```python
a = [[1, 2], [3, 4]]
```

### Step 3: Assign b = value

```python
b = [5, 6]
```

### Step 4: Assign c = value

```python
c = [0]
```

### Step 5: Assign manual_cartesian = np.array(...)

```python
manual_cartesian = np.array([[1, 2, 5, 0], [1, 2, 6, 0], [3, 4, 5, 0], [3, 4, 6, 0]])
```

### Step 6: Assign auto_cart = cartesian(...)

```python
auto_cart = cartesian(a, b, c)
```

### Step 7: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(manual_cartesian, auto_cart)
```


## Complete Example

```python
# Workflow
np.random.seed(1)
a = [[1, 2], [3, 4]]
b = [5, 6]
c = [0]
manual_cartesian = np.array([[1, 2, 5, 0], [1, 2, 6, 0], [3, 4, 5, 0], [3, 4, 6, 0]])
auto_cart = cartesian(a, b, c)
np.testing.assert_array_equal(manual_cartesian, auto_cart)
```

## Next Steps


---

*Source: test_math.py:73 | Complexity: Intermediate | Last updated: 2026-05-18*