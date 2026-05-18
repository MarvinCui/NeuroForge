# How To: Solve 2D Symmetric Positive Definite

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test solve 2d symmetric positive definite

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign bs = value

```python
bs = [np.array([1.1, 2.2]), np.array([0.01, 0.003]), np.array([100.0, 1000.0]), np.array([1e-05, 100000.0])]
```

**Verification:**
```python
assert_allclose(expected, actual, rtol=1e-09, atol=1e-09)
```

### Step 2: Assign As = value

```python
As = []
```

### Step 3: Assign identity = np.array(...)

```python
identity = np.array([1.0, 0.0, 1.0])
```

### Step 4: Call As.append()

```python
As.append(identity)
```

### Step 5: Assign small_det = np.array(...)

```python
small_det = np.array([0.001, 0.0001, 0.001])
```

### Step 6: Call As.append()

```python
As.append(small_det)
```

### Step 7: Assign large_det = np.array(...)

```python
large_det = np.array([1000000.0, 10000.0, 1000000.0])
```

### Step 8: Call As.append()

```python
As.append(large_det)
```

### Step 9: Assign AA = np.array(...)

```python
AA = np.array([[A[0], A[1]], [A[1], A[2]]])
```

### Step 10: Assign det = np.linalg.det(...)

```python
det = np.linalg.det(AA)
```

### Step 11: Assign expected = np.linalg.solve(...)

```python
expected = np.linalg.solve(AA, b)
```

### Step 12: Assign actual = ssd.solve_2d_symmetric_positive_definite(...)

```python
actual = ssd.solve_2d_symmetric_positive_definite(A, b, det)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(expected, actual, rtol=1e-09, atol=1e-09)
```


## Complete Example

```python
# Workflow
bs = [np.array([1.1, 2.2]), np.array([0.01, 0.003]), np.array([100.0, 1000.0]), np.array([1e-05, 100000.0])]
As = []
identity = np.array([1.0, 0.0, 1.0])
As.append(identity)
small_det = np.array([0.001, 0.0001, 0.001])
As.append(small_det)
large_det = np.array([1000000.0, 10000.0, 1000000.0])
As.append(large_det)
for A in As:
    AA = np.array([[A[0], A[1]], [A[1], A[2]]])
    det = np.linalg.det(AA)
    for b in bs:
        expected = np.linalg.solve(AA, b)
        actual = ssd.solve_2d_symmetric_positive_definite(A, b, det)
        assert_allclose(expected, actual, rtol=1e-09, atol=1e-09)
```

## Next Steps


---

*Source: test_sumsqdiff.py:444 | Complexity: Advanced | Last updated: 2026-05-18*