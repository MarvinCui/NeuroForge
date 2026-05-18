# How To: Coef Shape

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test coef shape

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.datasets`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.image`
- `nilearn.masking`

**Setup Required:**
```python
# Fixtures: penalty, cls
```

## Step-by-Step Guide

### Step 1: Assign iris = load_iris(...)

```python
iris = load_iris()
```

**Verification:**
```python
assert model.coef_.ndim == 2
```

### Step 2: Assign unknown = value

```python
X, y = (iris.data, iris.target)
```

### Step 3: Assign unknown = to_niimgs(...)

```python
X, mask = to_niimgs(X, (2, 2, 2))
```

### Step 4: Assign model = cls.fit(...)

```python
model = cls(mask=mask, max_iter=3, penalty=penalty, alphas=1.0, standardize='zscore_sample').fit(X, y)
```

**Verification:**
```python
assert model.coef_.ndim == 2
```


## Complete Example

```python
# Setup
# Fixtures: penalty, cls

# Workflow
iris = load_iris()
X, y = (iris.data, iris.target)
X, mask = to_niimgs(X, (2, 2, 2))
model = cls(mask=mask, max_iter=3, penalty=penalty, alphas=1.0, standardize='zscore_sample').fit(X, y)
assert model.coef_.ndim == 2
```

## Next Steps


---

*Source: test_same_api.py:317 | Complexity: Intermediate | Last updated: 2026-05-18*