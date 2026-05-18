# How To: Geometric Mean Properties Evaluate Convergence

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test geometric mean properties evaluate convergence

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: p
```

## Step-by-Step Guide

### Step 1: Assign n_matrices = 40

```python
n_matrices = 40
```

### Step 2: Assign n_features = 15

```python
n_features = 15
```

### Step 3: Assign spds = value

```python
spds = [random_spd(n_features, eig_min=0.01, cond=1000000.0, random_state=0) for _ in range(int(p * n_matrices))]
```

### Step 4: Call spds.extend()

```python
spds.extend((random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(int(p * n_matrices), n_matrices)))
```

### Step 5: Assign max_iter = value

```python
max_iter = 30 if p < 1 else 60
```

### Step 6: Call _geometric_mean()

```python
_geometric_mean(spds, max_iter=max_iter, tol=1e-05)
```


## Complete Example

```python
# Setup
# Fixtures: p

# Workflow
n_matrices = 40
n_features = 15
spds = [random_spd(n_features, eig_min=0.01, cond=1000000.0, random_state=0) for _ in range(int(p * n_matrices))]
spds.extend((random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(int(p * n_matrices), n_matrices)))
max_iter = 30 if p < 1 else 60
_geometric_mean(spds, max_iter=max_iter, tol=1e-05)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:472 | Complexity: Intermediate | Last updated: 2026-05-18*