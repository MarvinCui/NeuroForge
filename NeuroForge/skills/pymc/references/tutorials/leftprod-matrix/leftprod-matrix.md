# How To: Leftprod Matrix

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test leftprod matrix

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pymc`
- `pymc.math`


## Step-by-Step Guide

### Step 1: Assign X = value

```python
X = np.linspace(0, 1, 3)[:, None]
```

**Verification:**
```python
assert np.allclose(K, K_true)
```

### Step 2: Assign M = np.array(...)

```python
M = np.array([[1, 2, 3], [2, 1, 2], [3, 2, 1]])
```

### Step 3: Assign K = cov.eval(...)

```python
K = cov(X).eval()
```

### Step 4: Assign K_true = cov_true.eval(...)

```python
K_true = cov_true(X).eval()
```

**Verification:**
```python
assert np.allclose(K, K_true)
```

### Step 5: Assign cov = value

```python
cov = M + pm.gp.cov.ExpQuad(1, 0.1)
```

### Step 6: Assign cov_true = value

```python
cov_true = pm.gp.cov.ExpQuad(1, 0.1) + M
```


## Complete Example

```python
# Workflow
X = np.linspace(0, 1, 3)[:, None]
M = np.array([[1, 2, 3], [2, 1, 2], [3, 2, 1]])
with pm.Model() as model:
    cov = M + pm.gp.cov.ExpQuad(1, 0.1)
    cov_true = pm.gp.cov.ExpQuad(1, 0.1) + M
K = cov(X).eval()
K_true = cov_true(X).eval()
assert np.allclose(K, K_true)
```

## Next Steps


---

*Source: test_cov.py:85 | Complexity: Intermediate | Last updated: 2026-05-18*