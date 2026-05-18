# How To: Split Gof Meg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test GOF splitting on MEG data.

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
# Fixtures: forward, idx, weights
```

## Step-by-Step Guide

### Step 1: 'Test GOF splitting on MEG data.'

```python
'Test GOF splitting on MEG data.'
```

**Verification:**
```python
assert_array_less(prods, 0.005)
```

### Step 2: Assign gain = value

```python
gain = forward['sol']['data'][:, idx]
```

**Verification:**
```python
assert_allclose(gof_split.sum(0), 100.0, atol=1e-05)
```

### Step 3: Assign norms = np.linalg.norm(...)

```python
norms = np.linalg.norm(gain, axis=0)
```

**Verification:**
```python
assert_allclose(gof_split, 100 * np.eye(len(weights)), atol=1)
```

### Step 4: Assign triu = np.triu_indices(...)

```python
triu = np.triu_indices(len(idx), 1)
```

**Verification:**
```python
assert x.shape == (gain.shape[0], 1)
```

### Step 5: Assign prods = value

```python
prods = np.abs(np.dot(gain.T, gain) / np.outer(norms, norms))[triu]
```

**Verification:**
```python
assert_allclose(gof_split, want, atol=0.001, rtol=0.01)
```

### Step 6: Call assert_array_less()

```python
assert_array_less(prods, 0.005)
```

**Verification:**
```python
assert_allclose(gof_split.sum(), 100, rtol=1e-05)
```

### Step 7: Assign M = value

```python
M = gain * weights
```

### Step 8: Assign gof_split = _split_gof(...)

```python
gof_split = _split_gof(M, np.diag(weights), gain)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(gof_split.sum(0), 100.0, atol=1e-05)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(gof_split, 100 * np.eye(len(weights)), atol=1)
```

### Step 11: Assign weights = value

```python
weights = np.array(weights)[:, np.newaxis]
```

### Step 12: Assign x = value

```python
x = gain @ weights
```

**Verification:**
```python
assert x.shape == (gain.shape[0], 1)
```

### Step 13: Assign gof_split = _split_gof(...)

```python
gof_split = _split_gof(x, weights, gain)
```

### Step 14: Assign want = value

```python
want = (norms * weights.T).T ** 2
```

### Step 15: Assign want = value

```python
want = 100 * want / want.sum()
```

### Step 16: Call assert_allclose()

```python
assert_allclose(gof_split, want, atol=0.001, rtol=0.01)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(gof_split.sum(), 100, rtol=1e-05)
```


## Complete Example

```python
# Setup
# Fixtures: forward, idx, weights

# Workflow
'Test GOF splitting on MEG data.'
gain = forward['sol']['data'][:, idx]
norms = np.linalg.norm(gain, axis=0)
triu = np.triu_indices(len(idx), 1)
prods = np.abs(np.dot(gain.T, gain) / np.outer(norms, norms))[triu]
assert_array_less(prods, 0.005)
M = gain * weights
gof_split = _split_gof(M, np.diag(weights), gain)
assert_allclose(gof_split.sum(0), 100.0, atol=1e-05)
assert_allclose(gof_split, 100 * np.eye(len(weights)), atol=1)
weights = np.array(weights)[:, np.newaxis]
x = gain @ weights
assert x.shape == (gain.shape[0], 1)
gof_split = _split_gof(x, weights, gain)
want = (norms * weights.T).T ** 2
want = 100 * want / want.sum()
assert_allclose(gof_split, want, atol=0.001, rtol=0.01)
assert_allclose(gof_split.sum(), 100, rtol=1e-05)
```

## Next Steps


---

*Source: test_mxne_inverse.py:475 | Complexity: Advanced | Last updated: 2026-05-18*