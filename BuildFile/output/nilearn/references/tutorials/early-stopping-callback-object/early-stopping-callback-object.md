# How To: Early Stopping Callback Object

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test early stopping callback object

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `sklearn.datasets`
- `sklearn.linear_model`
- `sklearn.linear_model._coordinate_descent`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.decoding._utils`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.decoding.tests._testing`
- `nilearn.decoding.tests.test_same_api`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, n_samples, n_features
```

## Step-by-Step Guide

### Step 1: Assign X_test = rng.standard_normal(...)

```python
X_test = rng.standard_normal((n_samples, n_features))
```

**Verification:**
```python
assert len(escb.test_scores) == counter + 1
```

### Step 2: Assign y_test = np.dot(...)

```python
y_test = np.dot(X_test, np.ones(n_features))
```

### Step 3: Assign w = np.zeros(...)

```python
w = np.zeros(n_features)
```

### Step 4: Assign escb = _EarlyStoppingCallback(...)

```python
escb = _EarlyStoppingCallback(X_test, y_test, False, verbose=0)
```

### Step 5: Assign k = min(...)

```python
k = min(counter, n_features - 1)
```

### Step 6: Assign unknown = 1

```python
w[k] = 1
```

### Step 7: Call escb()

```python
escb({'w': w, 'counter': counter})
```

**Verification:**
```python
assert len(escb.test_scores) == counter + 1
```

### Step 8: Assign unknown = value

```python
w[k - 1] = 1 - w[k - 1]
```


## Complete Example

```python
# Setup
# Fixtures: rng, n_samples, n_features

# Workflow
X_test = rng.standard_normal((n_samples, n_features))
y_test = np.dot(X_test, np.ones(n_features))
w = np.zeros(n_features)
escb = _EarlyStoppingCallback(X_test, y_test, False, verbose=0)
for counter in range(50):
    k = min(counter, n_features - 1)
    w[k] = 1
    if k > 0 and rng.random() > 0.9:
        w[k - 1] = 1 - w[k - 1]
    escb({'w': w, 'counter': counter})
    assert len(escb.test_scores) == counter + 1
    if counter > 20:
        w *= 0.0
```

## Next Steps


---

*Source: test_space_net.py:128 | Complexity: Advanced | Last updated: 2026-05-18*