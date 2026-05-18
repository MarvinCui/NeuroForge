# How To: Geometric Mean Properties

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test geometric mean properties

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
assert isinstance(spds, list)
```

### Step 2: Assign n_features = 15

```python
n_features = 15
```

**Verification:**
```python
assert_array_equal(spd, input_spd)
```

### Step 3: Assign spds = value

```python
spds = [random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(n_matrices)]
```

**Verification:**
```python
assert is_spd(gmean, decimal=7)
```

### Step 4: Assign input_spds = copy.copy(...)

```python
input_spds = copy.copy(spds)
```

### Step 5: Assign gmean = _geometric_mean(...)

```python
gmean = _geometric_mean(spds)
```

**Verification:**
```python
assert isinstance(spds, list)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(spd, input_spd)
```


## Complete Example

```python
# Workflow
n_matrices = 40
n_features = 15
spds = [random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(n_matrices)]
input_spds = copy.copy(spds)
gmean = _geometric_mean(spds)
assert isinstance(spds, list)
for spd, input_spd in zip(spds, input_spds, strict=False):
    assert_array_equal(spd, input_spd)
assert is_spd(gmean, decimal=7)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:302 | Complexity: Intermediate | Last updated: 2026-05-18*