# How To: Geometric Mean Geodesic

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test geometric mean geodesic

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

### Step 1: Assign n_matrices = 10

```python
n_matrices = 10
```

**Verification:**
```python
assert_array_almost_equal(_geometric_mean(spds), gmean)
```

### Step 2: Assign n_features = 6

```python
n_features = 6
```

### Step 3: Assign sym = value

```python
sym = np.arange(n_features) / np.linalg.norm(np.arange(n_features))
```

### Step 4: Assign sym = value

```python
sym = sym * sym[:, np.newaxis]
```

### Step 5: Assign times = np.arange(...)

```python
times = np.arange(n_matrices)
```

### Step 6: Assign non_singular = np.eye(...)

```python
non_singular = np.eye(n_features)
```

### Step 7: Assign unknown = np.array(...)

```python
non_singular[1:3, 1:3] = np.array([[-1, -0.5], [-0.5, -1]])
```

### Step 8: Assign spds = value

```python
spds = [non_singular.dot(_map_eigenvalues(np.exp, time * sym)).dot(non_singular.T) for time in times]
```

### Step 9: Assign gmean = non_singular.dot.dot(...)

```python
gmean = non_singular.dot(_map_eigenvalues(np.exp, times.mean() * sym)).dot(non_singular.T)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(_geometric_mean(spds), gmean)
```


## Complete Example

```python
# Workflow
n_matrices = 10
n_features = 6
sym = np.arange(n_features) / np.linalg.norm(np.arange(n_features))
sym = sym * sym[:, np.newaxis]
times = np.arange(n_matrices)
non_singular = np.eye(n_features)
non_singular[1:3, 1:3] = np.array([[-1, -0.5], [-0.5, -1]])
spds = [non_singular.dot(_map_eigenvalues(np.exp, time * sym)).dot(non_singular.T) for time in times]
gmean = non_singular.dot(_map_eigenvalues(np.exp, times.mean() * sym)).dot(non_singular.T)
assert_array_almost_equal(_geometric_mean(spds), gmean)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:282 | Complexity: Advanced | Last updated: 2026-05-18*