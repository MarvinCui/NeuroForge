# How To: Graph Net And Tv Same For Pure L1 Spacenet Regressor

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.
    

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
# Fixtures: standardize, decimal
```

## Step-by-Step Guide

### Step 1: 'Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.\n    '

```python
'Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.\n    '
```

**Verification:**
```python
assert_array_almost_equal(sl.coef_, tvl1.coef_, decimal=decimal)
```

### Step 2: Assign dim = value

```python
dim = (3, 3, 3)
```

### Step 3: Assign unknown = _make_data(...)

```python
X, y, _, mask = _make_data(masked=True, dim=dim)
```

### Step 4: Assign unknown = to_niimgs(...)

```python
X, mask = to_niimgs(X, dim)
```

### Step 5: Assign alpha = 0.1

```python
alpha = 0.1
```

### Step 6: Assign l1_ratio = 1.0

```python
l1_ratio = 1.0
```

### Step 7: Assign max_iter = 20

```python
max_iter = 20
```

### Step 8: Assign sl = SpaceNetRegressor.fit(...)

```python
sl = SpaceNetRegressor(alphas=alpha, l1_ratios=l1_ratio, penalty='graph-net', max_iter=max_iter, mask=mask, standardize=standardize).fit(X, y)
```

### Step 9: Assign tvl1 = SpaceNetRegressor.fit(...)

```python
tvl1 = SpaceNetRegressor(alphas=alpha, l1_ratios=l1_ratio, penalty='tv-l1', max_iter=max_iter, mask=mask, standardize=standardize).fit(X, y)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sl.coef_, tvl1.coef_, decimal=decimal)
```


## Complete Example

```python
# Setup
# Fixtures: standardize, decimal

# Workflow
'Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.\n    '
dim = (3, 3, 3)
X, y, _, mask = _make_data(masked=True, dim=dim)
X, mask = to_niimgs(X, dim)
alpha = 0.1
l1_ratio = 1.0
max_iter = 20
sl = SpaceNetRegressor(alphas=alpha, l1_ratios=l1_ratio, penalty='graph-net', max_iter=max_iter, mask=mask, standardize=standardize).fit(X, y)
tvl1 = SpaceNetRegressor(alphas=alpha, l1_ratios=l1_ratio, penalty='tv-l1', max_iter=max_iter, mask=mask, standardize=standardize).fit(X, y)
assert_array_almost_equal(sl.coef_, tvl1.coef_, decimal=decimal)
```

## Next Steps


---

*Source: test_same_api.py:281 | Complexity: Advanced | Last updated: 2026-05-18*