# How To: Geometric Mean Properties Check Invariance

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test geometric mean properties check invariance

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

### Step 1: Assign n_matrices = 40

```python
n_matrices = 40
```

**Verification:**
```python
assert_array_almost_equal(_geometric_mean(spds), gmean)
```

### Step 2: Assign n_features = 15

```python
n_features = 15
```

**Verification:**
```python
assert_array_almost_equal(_geometric_mean(spds_cong), non_singular.dot(gmean).dot(non_singular.T))
```

### Step 3: Assign spds = value

```python
spds = [random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(n_matrices)]
```

**Verification:**
```python
assert_array_almost_equal(_geometric_mean(spds_inv, init=init), linalg.inv(gmean))
```

### Step 4: Assign gmean = _geometric_mean(...)

```python
gmean = _geometric_mean(spds)
```

### Step 5: Call spds.reverse()

```python
spds.reverse()
```

### Step 6: Call spds.insert()

```python
spds.insert(0, spds[1])
```

### Step 7: Call spds.pop()

```python
spds.pop(2)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(_geometric_mean(spds), gmean)
```

### Step 9: Assign non_singular = random_non_singular(...)

```python
non_singular = random_non_singular(n_features, random_state=0)
```

### Step 10: Assign spds_cong = value

```python
spds_cong = [non_singular.dot(spd).dot(non_singular.T) for spd in spds]
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(_geometric_mean(spds_cong), non_singular.dot(gmean).dot(non_singular.T))
```

### Step 12: Assign spds_inv = value

```python
spds_inv = [linalg.inv(spd) for spd in spds]
```

### Step 13: Assign init = linalg.inv(...)

```python
init = linalg.inv(np.mean(spds, axis=0))
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(_geometric_mean(spds_inv, init=init), linalg.inv(gmean))
```


## Complete Example

```python
# Workflow
n_matrices = 40
n_features = 15
spds = [random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(n_matrices)]
gmean = _geometric_mean(spds)
spds.reverse()
spds.insert(0, spds[1])
spds.pop(2)
assert_array_almost_equal(_geometric_mean(spds), gmean)
non_singular = random_non_singular(n_features, random_state=0)
spds_cong = [non_singular.dot(spd).dot(non_singular.T) for spd in spds]
assert_array_almost_equal(_geometric_mean(spds_cong), non_singular.dot(gmean).dot(non_singular.T))
spds_inv = [linalg.inv(spd) for spd in spds]
init = linalg.inv(np.mean(spds, axis=0))
assert_array_almost_equal(_geometric_mean(spds_inv, init=init), linalg.inv(gmean))
```

## Next Steps


---

*Source: test_connectivity_matrices.py:354 | Complexity: Advanced | Last updated: 2026-05-18*