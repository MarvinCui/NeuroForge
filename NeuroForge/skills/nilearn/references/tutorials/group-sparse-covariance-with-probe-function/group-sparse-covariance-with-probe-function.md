# How To: Group Sparse Covariance With Probe Function

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test group sparse covariance with probe function

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.connectome`
- `nilearn.connectome.group_sparse_cov`

**Setup Required:**
```python
# Fixtures: rng, duality_gap
```

## Step-by-Step Guide

### Step 1: Assign unknown = generate_group_sparse_gaussian_graphs(...)

```python
signals, _, _ = generate_group_sparse_gaussian_graphs(density=0.1, n_subjects=5, n_features=10, min_n_samples=100, max_n_samples=151, random_state=rng)
```

**Verification:**
```python
assert len(objective) == 4
```

### Step 2: Assign alpha = 0.1

```python
alpha = 0.1
```

**Verification:**
```python
assert np.all(np.diff(objective) <= 0)
```

### Step 3: Assign probe = Probe(...)

```python
probe = Probe()
```

**Verification:**
```python
assert omega.shape == (10, 10, 5)
```

### Step 4: Assign unknown = group_sparse_covariance(...)

```python
_, omega = group_sparse_covariance(signals, alpha, max_iter=4, tol=None, probe_function=probe)
```

### Step 5: Assign objective = value

```python
objective = probe.objective
```

**Verification:**
```python
assert len(objective) == 4
```

### Step 6: Assign self.objective = value

```python
self.objective = []
```

### Step 7: Call self.objective.append()

```python
self.objective.append(objective)
```

### Step 8: Assign unknown = group_sparse_scores(...)

```python
_, objective, _ = group_sparse_scores(omega, n_samples, emp_covs, alpha, duality_gap=duality_gap)
```

### Step 9: Assign unknown = group_sparse_scores(...)

```python
_, objective = group_sparse_scores(omega, n_samples, emp_covs, alpha, duality_gap=duality_gap)
```


## Complete Example

```python
# Setup
# Fixtures: rng, duality_gap

# Workflow
signals, _, _ = generate_group_sparse_gaussian_graphs(density=0.1, n_subjects=5, n_features=10, min_n_samples=100, max_n_samples=151, random_state=rng)
alpha = 0.1

class Probe:

    def __init__(self):
        self.objective = []

    def __call__(self, emp_covs, n_samples, alpha, max_iter, tol, n, omega, omega_diff):
        if n >= 0:
            if duality_gap:
                _, objective, _ = group_sparse_scores(omega, n_samples, emp_covs, alpha, duality_gap=duality_gap)
            else:
                _, objective = group_sparse_scores(omega, n_samples, emp_covs, alpha, duality_gap=duality_gap)
            self.objective.append(objective)
probe = Probe()
_, omega = group_sparse_covariance(signals, alpha, max_iter=4, tol=None, probe_function=probe)
objective = probe.objective
assert len(objective) == 4
assert np.all(np.diff(objective) <= 0)
assert omega.shape == (10, 10, 5)
```

## Next Steps


---

*Source: test_group_sparse_cov.py:93 | Complexity: Advanced | Last updated: 2026-05-18*