# How To: Add

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test add

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `pymc`


## Step-by-Step Guide

### Step 1: Assign X = value

```python
X = np.linspace(0, 1, 10)[:, None]
```

### Step 2: Assign M = mean.eval(...)

```python
M = mean(X).eval()
```

### Step 3: Call npt.assert_allclose()

```python
npt.assert_allclose(M[1], 0.7222 + 2 + 2, atol=0.001)
```

### Step 4: Assign mean1 = pm.gp.mean.Linear(...)

```python
mean1 = pm.gp.mean.Linear(coeffs=2, intercept=0.5)
```

### Step 5: Assign mean2 = pm.gp.mean.Constant(...)

```python
mean2 = pm.gp.mean.Constant(2)
```

### Step 6: Assign mean = value

```python
mean = mean1 + mean2 + mean2
```


## Complete Example

```python
# Workflow
X = np.linspace(0, 1, 10)[:, None]
with pm.Model() as model:
    mean1 = pm.gp.mean.Linear(coeffs=2, intercept=0.5)
    mean2 = pm.gp.mean.Constant(2)
    mean = mean1 + mean2 + mean2
M = mean(X).eval()
npt.assert_allclose(M[1], 0.7222 + 2 + 2, atol=0.001)
```

## Next Steps


---

*Source: test_mean.py:52 | Complexity: Intermediate | Last updated: 2026-05-18*