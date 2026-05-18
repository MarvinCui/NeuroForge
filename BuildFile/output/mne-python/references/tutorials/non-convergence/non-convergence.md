# How To: Non Convergence

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test non-convergence of MxNE solver to catch unexpected bugs.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.inverse_sparse.mxne_optim`
- `mne.time_frequency._stft`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test non-convergence of MxNE solver to catch unexpected bugs.'

```python
'Test non-convergence of MxNE solver to catch unexpected bugs.'
```

**Verification:**
```python
assert 'Convergence reached' not in log
```

### Step 2: Assign unknown = value

```python
n, p, t, alpha = (30, 40, 20, 1.0)
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 4: Assign G = rng.randn(...)

```python
G = rng.randn(n, p)
```

### Step 5: Assign X = np.zeros(...)

```python
X = np.zeros((p, t))
```

### Step 6: Assign unknown = 3

```python
X[0] = 3
```

### Step 7: Assign unknown = value

```python
X[4] = -2
```

### Step 8: Assign M = np.dot(...)

```python
M = np.dot(G, X)
```

### Step 9: Assign args = value

```python
args = (M, G, alpha, 1, 1e-12)
```

### Step 10: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'Convergence reached' not in log
```

### Step 11: Call mixed_norm_solver()

```python
mixed_norm_solver(*args, active_set_size=None, debias=True, solver='bcd', verbose=True)
```


## Complete Example

```python
# Workflow
'Test non-convergence of MxNE solver to catch unexpected bugs.'
n, p, t, alpha = (30, 40, 20, 1.0)
rng = np.random.RandomState(0)
G = rng.randn(n, p)
G /= np.std(G, axis=0)[None, :]
X = np.zeros((p, t))
X[0] = 3
X[4] = -2
M = np.dot(G, X)
args = (M, G, alpha, 1, 1e-12)
with catch_logging() as log:
    mixed_norm_solver(*args, active_set_size=None, debias=True, solver='bcd', verbose=True)
log = log.getvalue()
assert 'Convergence reached' not in log
```

## Next Steps


---

*Source: test_mxne_optim.py:121 | Complexity: Advanced | Last updated: 2026-05-18*