# How To: Rightadd Scalar

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rightadd scalar

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

### Step 2: Assign K = cov.eval(...)

```python
K = cov(X).eval()
```

### Step 3: Call npt.assert_allclose()

```python
npt.assert_allclose(K[0, 1], 1.5394, atol=0.001)
```

### Step 4: Assign Kd = cov.eval(...)

```python
Kd = cov(X, diag=True).eval()
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(np.diag(K), Kd, atol=1e-05)
```

### Step 6: Assign a = 1

```python
a = 1
```

### Step 7: Assign cov = value

```python
cov = pm.gp.cov.ExpQuad(1, 0.1) + a
```


## Complete Example

```python
# Workflow
X = np.linspace(0, 1, 10)[:, None]
with pm.Model() as model:
    a = 1
    cov = pm.gp.cov.ExpQuad(1, 0.1) + a
K = cov(X).eval()
npt.assert_allclose(K[0, 1], 1.5394, atol=0.001)
Kd = cov(X, diag=True).eval()
npt.assert_allclose(np.diag(K), Kd, atol=1e-05)
```

## Next Steps


---

*Source: test_cov.py:41 | Complexity: Intermediate | Last updated: 2026-05-18*