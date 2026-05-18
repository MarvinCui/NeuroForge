# How To: Mxne Inverse Sure Synthetic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests SURE criterion for automatic alpha selection on synthetic data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.datasets`
- `mne.dipole`
- `mne.inverse_sparse`
- `mne.inverse_sparse.mxne_inverse`
- `mne.inverse_sparse.mxne_optim`
- `mne.label`
- `mne.minimum_norm`
- `mne.minimum_norm.tests.test_inverse`
- `mne.simulation`
- `mne.source_estimate`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: n_sensors, n_dipoles, n_times, nnz, corr, n_orient, snr
```

## Step-by-Step Guide

### Step 1: 'Tests SURE criterion for automatic alpha selection on synthetic data.'

```python
'Tests SURE criterion for automatic alpha selection on synthetic data.'
```

**Verification:**
```python
assert np.count_nonzero(active_set, axis=-1) == n_orient * nnz
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 3: Assign sigma = np.sqrt(...)

```python
sigma = np.sqrt(1 - corr ** 2)
```

### Step 4: Assign U = rng.randn(...)

```python
U = rng.randn(n_sensors)
```

### Step 5: Assign G = np.empty(...)

```python
G = np.empty([n_sensors, n_dipoles], order='F')
```

### Step 6: Assign unknown = np.expand_dims(...)

```python
G[:, :n_orient] = np.expand_dims(U, axis=-1)
```

### Step 7: Assign n_dip_per_pos = value

```python
n_dip_per_pos = n_dipoles // n_orient
```

### Step 8: Assign support = rng.choice(...)

```python
support = rng.choice(n_dip_per_pos, nnz, replace=False)
```

### Step 9: Assign X = np.zeros(...)

```python
X = np.zeros((n_dipoles, n_times))
```

### Step 10: Assign M = value

```python
M = G @ X
```

### Step 11: Assign noise = rng.randn(...)

```python
noise = rng.randn(n_sensors, n_times)
```

### Step 12: Assign sigma = value

```python
sigma = 1 / np.linalg.norm(noise) * np.linalg.norm(M) / snr
```

### Step 13: Assign alpha_max = norm_l2inf(...)

```python
alpha_max = norm_l2inf(np.dot(G.T, M), n_orient, copy=False)
```

### Step 14: Assign alpha_grid = np.geomspace(...)

```python
alpha_grid = np.geomspace(alpha_max, alpha_max / 10, num=15)
```

### Step 15: Assign unknown = _compute_mxne_sure(...)

```python
_, active_set, _ = _compute_mxne_sure(M, G, alpha_grid, sigma=sigma, n_mxne_iter=5, maxit=3000, tol=0.0001, n_orient=n_orient, active_set_size=10, debias=True, solver='auto', dgap_freq=10, random_state=0, verbose=False)
```

**Verification:**
```python
assert np.count_nonzero(active_set, axis=-1) == n_orient * nnz
```

### Step 16: Assign unknown = np.expand_dims(...)

```python
G[:, j * n_orient:(j + 1) * n_orient] = np.expand_dims(U, axis=-1)
```

### Step 17: Assign unknown = rng.normal(...)

```python
X[k * n_orient:(k + 1) * n_orient, :] = rng.normal(size=(n_orient, n_times))
```


## Complete Example

```python
# Setup
# Fixtures: n_sensors, n_dipoles, n_times, nnz, corr, n_orient, snr

# Workflow
'Tests SURE criterion for automatic alpha selection on synthetic data.'
rng = np.random.RandomState(0)
sigma = np.sqrt(1 - corr ** 2)
U = rng.randn(n_sensors)
G = np.empty([n_sensors, n_dipoles], order='F')
G[:, :n_orient] = np.expand_dims(U, axis=-1)
n_dip_per_pos = n_dipoles // n_orient
for j in range(1, n_dip_per_pos):
    U *= corr
    U += sigma * rng.randn(n_sensors)
    G[:, j * n_orient:(j + 1) * n_orient] = np.expand_dims(U, axis=-1)
support = rng.choice(n_dip_per_pos, nnz, replace=False)
X = np.zeros((n_dipoles, n_times))
for k in support:
    X[k * n_orient:(k + 1) * n_orient, :] = rng.normal(size=(n_orient, n_times))
M = G @ X
noise = rng.randn(n_sensors, n_times)
sigma = 1 / np.linalg.norm(noise) * np.linalg.norm(M) / snr
M += sigma * noise
alpha_max = norm_l2inf(np.dot(G.T, M), n_orient, copy=False)
alpha_grid = np.geomspace(alpha_max, alpha_max / 10, num=15)
_, active_set, _ = _compute_mxne_sure(M, G, alpha_grid, sigma=sigma, n_mxne_iter=5, maxit=3000, tol=0.0001, n_orient=n_orient, active_set_size=10, debias=True, solver='auto', dgap_freq=10, random_state=0, verbose=False)
assert np.count_nonzero(active_set, axis=-1) == n_orient * nnz
```

## Next Steps


---

*Source: test_mxne_inverse.py:509 | Complexity: Advanced | Last updated: 2026-05-18*