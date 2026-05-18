# How To: Ajd

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test approximate joint diagonalization.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.linear_model`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.svm`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.decoding.csp`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test approximate joint diagonalization.'

```python
'Test approximate joint diagonalization.'
```

**Verification:**
```python
assert_array_almost_equal(V, V_matlab)
```

### Step 2: Assign unknown = value

```python
n_times, n_channels = (10, 3)
```

### Step 3: Assign seed = np.random.RandomState(...)

```python
seed = np.random.RandomState(0)
```

### Step 4: Assign diags = value

```python
diags = 2.0 + 0.1 * seed.randn(n_times, n_channels)
```

### Step 5: Assign A = value

```python
A = 2 * seed.rand(n_channels, n_channels) - 1
```

### Step 6: Assign covmats = np.empty(...)

```python
covmats = np.empty((n_times, n_channels, n_channels))
```

### Step 7: Assign unknown = _ajd_pham(...)

```python
V, D = _ajd_pham(covmats)
```

### Step 8: Assign V_matlab = value

```python
V_matlab = [[-3.507280775058041, -5.498189967306344, 7.720624541198574], [0.69468901323461, 0.775690358505945, -1.162043086446043], [-0.592603135588066, -0.59899692569626, 1.009550086271192]]
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(V, V_matlab)
```

### Step 10: Assign unknown = np.dot(...)

```python
covmats[i] = np.dot(np.dot(A, np.diag(diags[i])), A.T)
```


## Complete Example

```python
# Workflow
'Test approximate joint diagonalization.'
n_times, n_channels = (10, 3)
seed = np.random.RandomState(0)
diags = 2.0 + 0.1 * seed.randn(n_times, n_channels)
A = 2 * seed.rand(n_channels, n_channels) - 1
A /= np.atleast_2d(np.sqrt(np.sum(A ** 2, 1))).T
covmats = np.empty((n_times, n_channels, n_channels))
for i in range(n_times):
    covmats[i] = np.dot(np.dot(A, np.diag(diags[i])), A.T)
V, D = _ajd_pham(covmats)
V_matlab = [[-3.507280775058041, -5.498189967306344, 7.720624541198574], [0.69468901323461, 0.775690358505945, -1.162043086446043], [-0.592603135588066, -0.59899692569626, 1.009550086271192]]
assert_array_almost_equal(V, V_matlab)
```

## Next Steps


---

*Source: test_csp.py:396 | Complexity: Advanced | Last updated: 2026-05-18*