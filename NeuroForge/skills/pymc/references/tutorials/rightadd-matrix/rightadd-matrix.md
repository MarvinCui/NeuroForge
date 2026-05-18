# How To: Rightadd Matrix

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rightadd matrix

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
X = np.linspace(0, 1, 10)[:, None]
```

### Step 2: Assign M = value

```python
M = 2 * np.ones((10, 10))
```

### Step 3: Assign K = cov.eval(...)

```python
K = cov(X).eval()
```

### Step 4: Call npt.assert_allclose()

```python
npt.assert_allclose(K[0, 1], 2.5394, atol=0.001)
```

### Step 5: Assign Kd = cov.eval(...)

```python
Kd = cov(X, diag=True).eval()
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(np.diag(K), Kd, atol=1e-05)
```

### Step 7: Assign cov = value

```python
cov = pm.gp.cov.ExpQuad(1, 0.1) + M
```


## Complete Example

```python
# Workflow
X = np.linspace(0, 1, 10)[:, None]
M = 2 * np.ones((10, 10))
with pm.Model() as model:
    cov = pm.gp.cov.ExpQuad(1, 0.1) + M
K = cov(X).eval()
npt.assert_allclose(K[0, 1], 2.5394, atol=0.001)
Kd = cov(X, diag=True).eval()
npt.assert_allclose(np.diag(K), Kd, atol=1e-05)
```

## Next Steps


---

*Source: test_cov.py:63 | Complexity: Intermediate | Last updated: 2026-05-18*