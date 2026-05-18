# How To: Solve 3D Symmetric Positive Definite

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test solve 3d symmetric positive definite

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign bs = value

```python
bs = [np.array([1.1, 2.2, 3.3]), np.array([0.01, 0.003, 0.02]), np.array([100.0, 1000.0, 0.05]), np.array([1e-05, 100000.0, 1.0])]
```

**Verification:**
```python
assert_equal(is_singular, 1)
```

### Step 2: Assign taus = value

```python
taus = [0.0, 1.0, 0.0001, 100000.0]
```

**Verification:**
```python
assert_allclose(expected, actual, rtol=1e-09, atol=1e-09)
```

### Step 3: Assign gs = value

```python
gs = []
```

### Step 4: Assign diag = np.array(...)

```python
diag = np.array([0.0, 0.0, 0.0])
```

### Step 5: Call gs.append()

```python
gs.append(diag)
```

### Step 6: Call gs.append()

```python
gs.append(np.array([1.0, 0.0, 0.0]))
```

### Step 7: Call gs.append()

```python
gs.append(np.array([0.0, 1.0, 0.0]))
```

### Step 8: Call gs.append()

```python
gs.append(np.array([0.0, 0.0, 1.0]))
```

### Step 9: Call gs.append()

```python
gs.append(np.array([1.0, 0.5, 0.0]))
```

### Step 10: Call gs.append()

```python
gs.append(np.array([0.0, 0.2, 0.1]))
```

### Step 11: Call gs.append()

```python
gs.append(np.array([0.3, 0.0, 0.9]))
```

### Step 12: Assign A = value

```python
A = g[:, None] * g[None, :]
```

### Step 13: Assign AA = value

```python
AA = A + tau * np.eye(3)
```

### Step 14: Assign unknown = ssd.solve_3d_symmetric_positive_definite(...)

```python
actual, is_singular = ssd.solve_3d_symmetric_positive_definite(g, b, tau)
```

### Step 15: Call assert_equal()

```python
assert_equal(is_singular, 1)
```

### Step 16: Assign expected = np.linalg.solve(...)

```python
expected = np.linalg.solve(AA, b)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(expected, actual, rtol=1e-09, atol=1e-09)
```


## Complete Example

```python
# Workflow
bs = [np.array([1.1, 2.2, 3.3]), np.array([0.01, 0.003, 0.02]), np.array([100.0, 1000.0, 0.05]), np.array([1e-05, 100000.0, 1.0])]
taus = [0.0, 1.0, 0.0001, 100000.0]
gs = []
diag = np.array([0.0, 0.0, 0.0])
gs.append(diag)
gs.append(np.array([1.0, 0.0, 0.0]))
gs.append(np.array([0.0, 1.0, 0.0]))
gs.append(np.array([0.0, 0.0, 1.0]))
gs.append(np.array([1.0, 0.5, 0.0]))
gs.append(np.array([0.0, 0.2, 0.1]))
gs.append(np.array([0.3, 0.0, 0.9]))
for g in gs:
    A = g[:, None] * g[None, :]
    for tau in taus:
        AA = A + tau * np.eye(3)
        for b in bs:
            actual, is_singular = ssd.solve_3d_symmetric_positive_definite(g, b, tau)
            if tau == 0.0:
                assert_equal(is_singular, 1)
            else:
                expected = np.linalg.solve(AA, b)
                assert_allclose(expected, actual, rtol=1e-09, atol=1e-09)
```

## Next Steps


---

*Source: test_sumsqdiff.py:477 | Complexity: Advanced | Last updated: 2026-05-18*