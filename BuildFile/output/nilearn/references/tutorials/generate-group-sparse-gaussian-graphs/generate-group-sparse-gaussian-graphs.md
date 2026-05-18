# How To: Generate Group Sparse Gaussian Graphs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test generate group sparse gaussian graphs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `pandas.api.types`
- `pandas.testing`
- `nilearn._utils.data_gen`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: n_subjects, n_features, n_samples_range, density, rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = generate_group_sparse_gaussian_graphs(...)

```python
signals, precisions, topology = generate_group_sparse_gaussian_graphs(n_subjects=n_subjects, n_features=n_features, min_n_samples=n_samples_range[0], max_n_samples=n_samples_range[1], density=density, random_state=rng)
```

**Verification:**
```python
assert len(signals) == n_subjects
```

### Step 2: Assign signal_shapes = np.array(...)

```python
signal_shapes = np.array([s.shape for s in signals])
```

**Verification:**
```python
assert len(precisions) == n_subjects
```

### Step 3: Assign precision_shapes = np.array(...)

```python
precision_shapes = np.array([p.shape for p in precisions])
```

**Verification:**
```python
assert np.all((signal_shapes[:, 0] >= n_samples_range[0]) & (signal_shapes[:, 0] <= n_samples_range[1]))
```

### Step 4: Assign eigenvalues = np.array(...)

```python
eigenvalues = np.array([np.linalg.eigvalsh(p) for p in precisions])
```

**Verification:**
```python
assert np.all(signal_shapes[:, 1] == n_features)
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects, n_features, n_samples_range, density, rng

# Workflow
signals, precisions, topology = generate_group_sparse_gaussian_graphs(n_subjects=n_subjects, n_features=n_features, min_n_samples=n_samples_range[0], max_n_samples=n_samples_range[1], density=density, random_state=rng)
assert len(signals) == n_subjects
assert len(precisions) == n_subjects
signal_shapes = np.array([s.shape for s in signals])
precision_shapes = np.array([p.shape for p in precisions])
assert np.all((signal_shapes[:, 0] >= n_samples_range[0]) & (signal_shapes[:, 0] <= n_samples_range[1]))
assert np.all(signal_shapes[:, 1] == n_features)
assert np.all(precision_shapes == (n_features, n_features))
assert topology.shape == (n_features, n_features)
eigenvalues = np.array([np.linalg.eigvalsh(p) for p in precisions])
assert np.all(eigenvalues >= 0)
```

## Next Steps


---

*Source: test_data_gen.py:652 | Complexity: Intermediate | Last updated: 2026-05-18*