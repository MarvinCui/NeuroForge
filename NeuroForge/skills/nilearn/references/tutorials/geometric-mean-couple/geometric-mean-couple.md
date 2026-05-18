# How To: Geometric Mean Couple

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test geometric mean couple

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

### Step 1: Assign n_features = 7

```python
n_features = 7
```

**Verification:**
```python
assert_array_almost_equal(_geometric_mean([spd1, spd2]), geo)
```

### Step 2: Assign spd1 = np.ones(...)

```python
spd1 = np.ones((n_features, n_features))
```

### Step 3: Assign spd1 = value

```python
spd1 = spd1.dot(spd1) + n_features * np.eye(n_features)
```

### Step 4: Assign spd2 = np.tril(...)

```python
spd2 = np.tril(np.ones((n_features, n_features)))
```

### Step 5: Assign spd2 = spd2.dot(...)

```python
spd2 = spd2.dot(spd2.T)
```

### Step 6: Assign unknown = np.linalg.eigh(...)

```python
vals_spd2, vecs_spd2 = np.linalg.eigh(spd2)
```

### Step 7: Assign spd2_sqrt = _form_symmetric(...)

```python
spd2_sqrt = _form_symmetric(np.sqrt, vals_spd2, vecs_spd2)
```

### Step 8: Assign spd2_inv_sqrt = _form_symmetric(...)

```python
spd2_inv_sqrt = _form_symmetric(np.sqrt, 1.0 / vals_spd2, vecs_spd2)
```

### Step 9: Assign geo = spd2_sqrt.dot.dot(...)

```python
geo = spd2_sqrt.dot(_map_eigenvalues(np.sqrt, spd2_inv_sqrt.dot(spd1).dot(spd2_inv_sqrt))).dot(spd2_sqrt)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(_geometric_mean([spd1, spd2]), geo)
```


## Complete Example

```python
# Workflow
n_features = 7
spd1 = np.ones((n_features, n_features))
spd1 = spd1.dot(spd1) + n_features * np.eye(n_features)
spd2 = np.tril(np.ones((n_features, n_features)))
spd2 = spd2.dot(spd2.T)
vals_spd2, vecs_spd2 = np.linalg.eigh(spd2)
spd2_sqrt = _form_symmetric(np.sqrt, vals_spd2, vecs_spd2)
spd2_inv_sqrt = _form_symmetric(np.sqrt, 1.0 / vals_spd2, vecs_spd2)
geo = spd2_sqrt.dot(_map_eigenvalues(np.sqrt, spd2_inv_sqrt.dot(spd1).dot(spd2_inv_sqrt))).dot(spd2_sqrt)
assert_array_almost_equal(_geometric_mean([spd1, spd2]), geo)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:250 | Complexity: Advanced | Last updated: 2026-05-18*