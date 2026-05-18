# How To: Logdiffexp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logdiffexp

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

### Step 1: Assign a = pt.vector(...)

```python
a = pt.vector('a')
```

### Step 2: Assign b = pt.vector(...)

```python
b = pt.vector('b')
```

### Step 3: Assign a_test = np.log(...)

```python
a_test = np.log([1, 2, 3, 4])
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logdiffexp(a, b).eval({a: a_test, b: b_test}), 0, atol=1e-15)
```

### Step 5: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(logdiffexp(a, b).eval({a: [-np.inf, -np.inf, -1], b: [-1, -np.inf, -np.inf]}), [np.nan, -np.inf, -1])
```

### Step 6: Assign b_test = np.log(...)

```python
b_test = np.log([0, 1, 2, 3])
```


## Complete Example

```python
# Workflow
a = pt.vector('a')
b = pt.vector('b')
a_test = np.log([1, 2, 3, 4])
with np.errstate(divide='ignore'):
    b_test = np.log([0, 1, 2, 3])
np.testing.assert_allclose(logdiffexp(a, b).eval({a: a_test, b: b_test}), 0, atol=1e-15)
np.testing.assert_array_equal(logdiffexp(a, b).eval({a: [-np.inf, -np.inf, -1], b: [-1, -np.inf, -np.inf]}), [np.nan, -np.inf, -1])
```

## Next Steps


---

*Source: test_math.py:143 | Complexity: Intermediate | Last updated: 2026-05-18*