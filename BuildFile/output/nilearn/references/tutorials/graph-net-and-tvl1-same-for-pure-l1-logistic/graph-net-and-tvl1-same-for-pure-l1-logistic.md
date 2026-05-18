# How To: Graph Net And Tvl1 Same For Pure L1 Logistic

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check graph_net_solver and tvl1_solver should give same results     when l1_ratio = 1.
    

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
# Fixtures: max_iter, decimal
```

## Step-by-Step Guide

### Step 1: 'Check graph_net_solver and tvl1_solver should give same results     when l1_ratio = 1.\n    '

```python
'Check graph_net_solver and tvl1_solver should give same results     when l1_ratio = 1.\n    '
```

**Verification:**
```python
assert_array_almost_equal(a, b, decimal=decimal)
```

### Step 2: Assign iris = load_iris(...)

```python
iris = load_iris()
```

### Step 3: Assign unknown = value

```python
X, y = (iris.data, iris.target)
```

### Step 4: Assign y = value

```python
y = y > 0.0
```

### Step 5: Assign alpha = value

```python
alpha = 1.0 / X.shape[0]
```

### Step 6: Assign unknown = to_niimgs(...)

```python
_, mask_ = to_niimgs(X, (2, 2, 2))
```

### Step 7: Assign mask = get_data.astype.ravel(...)

```python
mask = get_data(mask_).astype(bool).ravel()
```

### Step 8: Assign a = value

```python
a = graph_net_logistic(X, y, alpha, l1_ratio=1.0, mask=mask, max_iter=max_iter, verbose=0)[0]
```

### Step 9: Assign b = value

```python
b = tvl1_solver(X, y, alpha, l1_ratio=1.0, loss='logistic', mask=mask, max_iter=max_iter, verbose=1)[0]
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(a, b, decimal=decimal)
```


## Complete Example

```python
# Setup
# Fixtures: max_iter, decimal

# Workflow
'Check graph_net_solver and tvl1_solver should give same results     when l1_ratio = 1.\n    '
iris = load_iris()
X, y = (iris.data, iris.target)
y = y > 0.0
alpha = 1.0 / X.shape[0]
_, mask_ = to_niimgs(X, (2, 2, 2))
mask = get_data(mask_).astype(bool).ravel()
a = graph_net_logistic(X, y, alpha, l1_ratio=1.0, mask=mask, max_iter=max_iter, verbose=0)[0]
b = tvl1_solver(X, y, alpha, l1_ratio=1.0, loss='logistic', mask=mask, max_iter=max_iter, verbose=1)[0]
assert_array_almost_equal(a, b, decimal=decimal)
```

## Next Steps


---

*Source: test_same_api.py:208 | Complexity: Advanced | Last updated: 2026-05-18*