# How To: Matrix Matrix Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test matrix matrix transform

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `pytensor.tensor.type`
- `pymc.distributions`
- `pymc.logprob.basic`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(46)
```

### Step 2: Assign unknown = value

```python
n, p = (2, 3)
```

### Step 3: Assign M = rng.normal(...)

```python
M = rng.normal(size=(n, p))
```

### Step 4: Assign A = value

```python
A = rng.normal(size=(n, n)) * 0.1
```

### Step 5: Assign U = value

```python
U = A.T @ A
```

### Step 6: Assign B = value

```python
B = rng.normal(size=(p, p)) * 0.1
```

### Step 7: Assign V = value

```python
V = B.T @ B
```

### Step 8: Assign X = MatrixNormal.dist(...)

```python
X = MatrixNormal.dist(mu=M, rowcov=U, colcov=V)
```

### Step 9: Assign D = rng.normal(...)

```python
D = rng.normal(size=(n, n))
```

### Step 10: Assign C = rng.normal(...)

```python
C = rng.normal(size=(p, p))
```

### Step 11: Assign Y = value

```python
Y = D @ X @ C
```

### Step 12: Assign ref_dist = MatrixNormal.dist(...)

```python
ref_dist = MatrixNormal.dist(mu=D @ M @ C, rowcov=D @ U @ D.T, colcov=C.T @ V @ C)
```

### Step 13: Assign test_Y = rng.normal(...)

```python
test_Y = rng.normal(size=(n, p))
```

### Step 14: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp(Y, test_Y).eval(), logp(ref_dist, test_Y).eval(), rtol=1e-05)
```


## Complete Example

```python
# Workflow
rng = np.random.default_rng(46)
n, p = (2, 3)
M = rng.normal(size=(n, p))
A = rng.normal(size=(n, n)) * 0.1
U = A.T @ A
B = rng.normal(size=(p, p)) * 0.1
V = B.T @ B
X = MatrixNormal.dist(mu=M, rowcov=U, colcov=V)
D = rng.normal(size=(n, n))
C = rng.normal(size=(p, p))
Y = D @ X @ C
ref_dist = MatrixNormal.dist(mu=D @ M @ C, rowcov=D @ U @ D.T, colcov=C.T @ V @ C)
test_Y = rng.normal(size=(n, p))
np.testing.assert_allclose(logp(Y, test_Y).eval(), logp(ref_dist, test_Y).eval(), rtol=1e-05)
```

## Next Steps


---

*Source: test_linalg.py:54 | Complexity: Advanced | Last updated: 2026-05-18*