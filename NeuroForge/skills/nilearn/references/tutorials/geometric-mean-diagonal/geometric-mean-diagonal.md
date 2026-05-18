# How To: Geometric Mean Diagonal

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test geometric mean diagonal

## Prerequisites

**Required Modules:**
- `copy`
- `warnings`
- `math`
- `numpy`
- `pytest`
- `numpy.testing`
- `pandas`
- `scipy`
- `sklearn.covariance`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.extmath`
- `nilearn._utils.versions`
- `nilearn.connectome.connectivity_matrices`
- `nilearn.tests.test_signal`


## Step-by-Step Guide

### Step 1: Assign n_matrices = 20

```python
n_matrices = 20
```

**Verification:**
```python
assert_array_almost_equal(_geometric_mean(diags), geo)
```

### Step 2: Assign n_features = 5

```python
n_features = 5
```

### Step 3: Assign diags = value

```python
diags = []
```

### Step 4: Assign geo = value

```python
geo = np.prod(np.array(diags), axis=0) ** (1 / float(len(diags)))
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(_geometric_mean(diags), geo)
```

### Step 6: Assign diag = np.eye(...)

```python
diag = np.eye(n_features)
```

### Step 7: Assign unknown = value

```python
diag[k % n_features, k % n_features] = 10000.0 + k
```

### Step 8: Assign unknown = value

```python
diag[(n_features - 1) // (k + 1), (n_features - 1) // (k + 1)] = (k + 1) * 0.0001
```

### Step 9: Call diags.append()

```python
diags.append(diag)
```


## Complete Example

```python
# Workflow
n_matrices = 20
n_features = 5
diags = []
for k in range(n_matrices):
    diag = np.eye(n_features)
    diag[k % n_features, k % n_features] = 10000.0 + k
    diag[(n_features - 1) // (k + 1), (n_features - 1) // (k + 1)] = (k + 1) * 0.0001
    diags.append(diag)
geo = np.prod(np.array(diags), axis=0) ** (1 / float(len(diags)))
assert_array_almost_equal(_geometric_mean(diags), geo)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:266 | Complexity: Advanced | Last updated: 2026-05-18*