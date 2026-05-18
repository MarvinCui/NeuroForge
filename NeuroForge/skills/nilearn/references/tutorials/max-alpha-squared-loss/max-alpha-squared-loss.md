# How To: Max Alpha Squared Loss

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests that models with L1 regularization over the theoretical bound     are full of zeros, for logistic regression.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `nibabel`
- `numpy.testing`
- `scipy`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.decoding.tests._testing`
- `test_same_api`

**Setup Required:**
```python
# Fixtures: estimator, l1_ratio
```

## Step-by-Step Guide

### Step 1: 'Tests that models with L1 regularization over the theoretical bound     are full of zeros, for logistic regression.\n    '

```python
'Tests that models with L1 regularization over the theoretical bound     are full of zeros, for logistic regression.\n    '
```

**Verification:**
```python
assert_almost_equal(reg.coef_, 0.0)
```

### Step 2: Assign unknown = _make_data(...)

```python
X, y, _, _, mask_, X_ = _make_data()
```

### Step 3: Assign reg = estimator(...)

```python
reg = estimator(mask=mask_, max_iter=10, penalty='graph-net', standardize='zscore_sample')
```

### Step 4: Assign reg.l1_ratios = l1_ratio

```python
reg.l1_ratios = l1_ratio
```

### Step 5: Assign reg.alphas = value

```python
reg.alphas = np.max(np.dot(X.T, y)) / l1_ratio
```

### Step 6: Call reg.fit()

```python
reg.fit(X_, y)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(reg.coef_, 0.0)
```


## Complete Example

```python
# Setup
# Fixtures: estimator, l1_ratio

# Workflow
'Tests that models with L1 regularization over the theoretical bound     are full of zeros, for logistic regression.\n    '
X, y, _, _, mask_, X_ = _make_data()
reg = estimator(mask=mask_, max_iter=10, penalty='graph-net', standardize='zscore_sample')
reg.l1_ratios = l1_ratio
reg.alphas = np.max(np.dot(X.T, y)) / l1_ratio
reg.fit(X_, y)
assert_almost_equal(reg.coef_, 0.0)
```

## Next Steps


---

*Source: test_graph_net.py:239 | Complexity: Intermediate | Last updated: 2026-05-18*