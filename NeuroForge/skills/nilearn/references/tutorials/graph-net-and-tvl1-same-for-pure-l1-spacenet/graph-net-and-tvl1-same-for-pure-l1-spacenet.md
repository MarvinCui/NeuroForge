# How To: Graph Net And Tvl1 Same For Pure L1 Spacenet

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.

Results should be exactly the same for pure lasso
However because of the TV-L1 prox approx, results might be 'slightly'
different.

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
# Fixtures: estimator, affine_eye, standardize, max_iter, decimal
```

## Step-by-Step Guide

### Step 1: "Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.\n\n    Results should be exactly the same for pure lasso\n    However because of the TV-L1 prox approx, results might be 'slightly'\n    different.\n    "

```python
"Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.\n\n    Results should be exactly the same for pure lasso\n    However because of the TV-L1 prox approx, results might be 'slightly'\n    different.\n    "
```

**Verification:**
```python
assert_array_almost_equal(sl.coef_, tvl1.coef_, decimal=decimal)
```

### Step 2: Assign unknown = _make_data(...)

```python
X, y, _, mask = _make_data(dim=(3, 3, 3))
```

### Step 3: Assign y = np.round(...)

```python
y = np.round(y)
```

### Step 4: Assign alpha = 0.01

```python
alpha = 0.01
```

### Step 5: Assign unmasked_X = np.rollaxis(...)

```python
unmasked_X = np.rollaxis(X, -1, start=0)
```

### Step 6: Assign unmasked_X = np.array(...)

```python
unmasked_X = np.array([x[mask] for x in unmasked_X])
```

### Step 7: Assign mask = Nifti1Image(...)

```python
mask = Nifti1Image(mask.astype(np.float64), affine_eye)
```

### Step 8: Assign X = Nifti1Image(...)

```python
X = Nifti1Image(X.astype(np.float64), affine_eye)
```

### Step 9: Assign sl = estimator.fit(...)

```python
sl = estimator(alphas=alpha, l1_ratios=1.0, mask=mask, penalty='graph-net', max_iter=max_iter, standardize=standardize).fit(X, y)
```

### Step 10: Assign tvl1 = estimator.fit(...)

```python
tvl1 = estimator(alphas=alpha, l1_ratios=1.0, mask=mask, penalty='tv-l1', max_iter=max_iter, standardize=standardize).fit(X, y)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sl.coef_, tvl1.coef_, decimal=decimal)
```


## Complete Example

```python
# Setup
# Fixtures: estimator, affine_eye, standardize, max_iter, decimal

# Workflow
"Check that graph_net_solver and tvl1_solver give same results     when l1_ratio = 1.\n\n    Results should be exactly the same for pure lasso\n    However because of the TV-L1 prox approx, results might be 'slightly'\n    different.\n    "
X, y, _, mask = _make_data(dim=(3, 3, 3))
y = np.round(y)
alpha = 0.01
unmasked_X = np.rollaxis(X, -1, start=0)
unmasked_X = np.array([x[mask] for x in unmasked_X])
mask = Nifti1Image(mask.astype(np.float64), affine_eye)
X = Nifti1Image(X.astype(np.float64), affine_eye)
sl = estimator(alphas=alpha, l1_ratios=1.0, mask=mask, penalty='graph-net', max_iter=max_iter, standardize=standardize).fit(X, y)
tvl1 = estimator(alphas=alpha, l1_ratios=1.0, mask=mask, penalty='tv-l1', max_iter=max_iter, standardize=standardize).fit(X, y)
assert_array_almost_equal(sl.coef_, tvl1.coef_, decimal=decimal)
```

## Next Steps


---

*Source: test_same_api.py:165 | Complexity: Advanced | Last updated: 2026-05-18*