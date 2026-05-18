# How To: Full Shape

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test full shape

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pymc`
- `pymc.math`

**Setup Required:**
```python
# Fixtures: kernel, args
```

## Step-by-Step Guide

### Step 1: Assign X = value

```python
X = np.arange(10)[:, None]
```

**Verification:**
```python
assert tuple(getattr(pm.gp.cov, kernel)(*args).full(X, Xs).shape.eval()) == (len(X), len(Xs))
```

### Step 2: Assign Xs = value

```python
Xs = np.arange(5)[:, None]
```

**Verification:**
```python
assert tuple(getattr(pm.gp.cov, kernel)(*args).full(X, Xs).shape.eval()) == (len(X), len(Xs))
```


## Complete Example

```python
# Setup
# Fixtures: kernel, args

# Workflow
X = np.arange(10)[:, None]
Xs = np.arange(5)[:, None]
assert tuple(getattr(pm.gp.cov, kernel)(*args).full(X, Xs).shape.eval()) == (len(X), len(Xs))
```

## Next Steps


---

*Source: test_cov.py:945 | Complexity: Beginner | Last updated: 2026-05-18*