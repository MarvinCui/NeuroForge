# How To: Graph Net And Tvl1 Same For Pure L1 Logistic Spacenet Classifier

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

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
# Fixtures: estimator, standardize, max_iter, decimal
```

## Step-by-Step Guide

### Step 1: 'Check graph_net_solver and tvl1_solver should give same results     when l1_ratio = 1.\n    '

```python
'Check graph_net_solver and tvl1_solver should give same results     when l1_ratio = 1.\n    '
```

**Verification:**
```python
assert_array_almost_equal(sl.coef_[0], tvl1.coef_[0], decimal=decimal)
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
X_, mask_ = to_niimgs(X, (2, 2, 2))
```

### Step 7: Assign sl = estimator.fit(...)

```python
sl = estimator(alphas=alpha, l1_ratios=1.0, max_iter=max_iter, mask=mask_, penalty='graph-net', standardize=standardize).fit(X_, y)
```

### Step 8: Assign tvl1 = estimator.fit(...)

```python
tvl1 = estimator(alphas=alpha, l1_ratios=1.0, max_iter=max_iter, mask=mask_, penalty='tv-l1', standardize=standardize).fit(X_, y)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sl.coef_[0], tvl1.coef_[0], decimal=decimal)
```


## Complete Example

```python
# Setup
# Fixtures: estimator, standardize, max_iter, decimal

# Workflow
'Check graph_net_solver and tvl1_solver should give same results     when l1_ratio = 1.\n    '
iris = load_iris()
X, y = (iris.data, iris.target)
y = y > 0.0
alpha = 1.0 / X.shape[0]
X_, mask_ = to_niimgs(X, (2, 2, 2))
sl = estimator(alphas=alpha, l1_ratios=1.0, max_iter=max_iter, mask=mask_, penalty='graph-net', standardize=standardize).fit(X_, y)
tvl1 = estimator(alphas=alpha, l1_ratios=1.0, max_iter=max_iter, mask=mask_, penalty='tv-l1', standardize=standardize).fit(X_, y)
assert_array_almost_equal(sl.coef_[0], tvl1.coef_[0], decimal=decimal)
```

## Next Steps


---

*Source: test_same_api.py:246 | Complexity: Advanced | Last updated: 2026-05-18*