# How To: Low Rank Methods

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test low-rank covariance matrix estimation.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `sys`
- `inspect`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.cov`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.rank`
- `mne.utils`
- `sklearn`

**Setup Required:**
```python
# Fixtures: rank, raw_epochs_events
```

## Step-by-Step Guide

### Step 1: 'Test low-rank covariance matrix estimation.'

```python
'Test low-rank covariance matrix estimation.'
```

**Verification:**
```python
assert this_rank == n_ch
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert this_rank == sss_proj_rank
```

### Step 3: Assign epochs = value

```python
epochs = raw_epochs_events[1]
```

**Verification:**
```python
assert these_bounds[0] < cov['loglik'] < these_bounds[1], (rank, method)
```

### Step 4: Assign sss_proj_rank = 139

```python
sss_proj_rank = 139
```

### Step 5: Assign n_ch = 366

```python
n_ch = 366
```

### Step 6: Assign methods = value

```python
methods = ('empirical', 'diagonal_fixed', 'oas')
```

### Step 7: Assign bounds = value

```python
bounds = {'None': dict(empirical=(-15000, -5000), diagonal_fixed=(-1500, -500), oas=(-700, -600)), 'full': dict(empirical=(-18000, -8000), diagonal_fixed=(-2000, -1600), oas=(-1600, -1000)), 'info': dict(empirical=(-15000, -5000), diagonal_fixed=(-700, -600), oas=(-700, -600))}
```

### Step 8: Assign covs = compute_covariance(...)

```python
covs = compute_covariance(epochs, method=methods, return_estimators=True, rank=rank, verbose=True)
```

### Step 9: Assign method = value

```python
method = cov['method']
```

### Step 10: Assign these_bounds = value

```python
these_bounds = bounds[str(rank)][method]
```

### Step 11: Assign this_rank = _cov_rank(...)

```python
this_rank = _cov_rank(cov, epochs.info, proj=rank != 'full')
```

**Verification:**
```python
assert these_bounds[0] < cov['loglik'] < these_bounds[1], (rank, method)
```


## Complete Example

```python
# Setup
# Fixtures: rank, raw_epochs_events

# Workflow
'Test low-rank covariance matrix estimation.'
pytest.importorskip('sklearn')
epochs = raw_epochs_events[1]
sss_proj_rank = 139
n_ch = 366
methods = ('empirical', 'diagonal_fixed', 'oas')
bounds = {'None': dict(empirical=(-15000, -5000), diagonal_fixed=(-1500, -500), oas=(-700, -600)), 'full': dict(empirical=(-18000, -8000), diagonal_fixed=(-2000, -1600), oas=(-1600, -1000)), 'info': dict(empirical=(-15000, -5000), diagonal_fixed=(-700, -600), oas=(-700, -600))}
with pytest.warns(RuntimeWarning, match='Too few samples'):
    covs = compute_covariance(epochs, method=methods, return_estimators=True, rank=rank, verbose=True)
for cov in covs:
    method = cov['method']
    these_bounds = bounds[str(rank)][method]
    this_rank = _cov_rank(cov, epochs.info, proj=rank != 'full')
    if rank == 'full' and method != 'empirical':
        assert this_rank == n_ch
    else:
        assert this_rank == sss_proj_rank
    assert these_bounds[0] < cov['loglik'] < these_bounds[1], (rank, method)
```

## Next Steps


---

*Source: test_cov.py:792 | Complexity: Advanced | Last updated: 2026-05-18*