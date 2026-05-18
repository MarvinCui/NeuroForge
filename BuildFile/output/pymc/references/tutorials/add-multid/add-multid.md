# How To: Add Multid

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test add multid

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `pymc`


## Step-by-Step Guide

### Step 1: Assign X = np.linspace.reshape(...)

```python
X = np.linspace(0, 1, 30).reshape(10, 3)
```

### Step 2: Assign A = np.array(...)

```python
A = np.array([1, 2, 3])
```

### Step 3: Assign b = 10

```python
b = 10
```

### Step 4: Assign M = mean.eval(...)

```python
M = mean(X).eval()
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(M[1], 10.8965 + 2 + 2, atol=0.001)
```

### Step 6: Assign mean1 = pm.gp.mean.Linear(...)

```python
mean1 = pm.gp.mean.Linear(coeffs=A, intercept=b)
```

### Step 7: Assign mean2 = pm.gp.mean.Constant(...)

```python
mean2 = pm.gp.mean.Constant(2)
```

### Step 8: Assign mean = value

```python
mean = mean1 + mean2 + mean2
```


## Complete Example

```python
# Workflow
X = np.linspace(0, 1, 30).reshape(10, 3)
A = np.array([1, 2, 3])
b = 10
with pm.Model() as model:
    mean1 = pm.gp.mean.Linear(coeffs=A, intercept=b)
    mean2 = pm.gp.mean.Constant(2)
    mean = mean1 + mean2 + mean2
M = mean(X).eval()
npt.assert_allclose(M[1], 10.8965 + 2 + 2, atol=0.001)
```

## Next Steps


---

*Source: test_mean.py:70 | Complexity: Advanced | Last updated: 2026-05-18*