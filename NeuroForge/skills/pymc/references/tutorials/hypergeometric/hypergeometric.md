# How To: Hypergeometric

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test hypergeometric

## Prerequisites

**Required Modules:**
- `functools`
- `itertools`
- `sys`
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.tensor`
- `pymc`
- `pymc.distributions.discrete`
- `pymc.exceptions`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign N_domain = Domain(...)

```python
N_domain = Domain([0, 10, 20, 30, np.inf], dtype='int64')
```

### Step 2: Assign n_domain, k_domain = Domain(...)

```python
n_domain = k_domain = Domain([0, 1, 2, 3, np.inf], dtype='int64')
```

### Step 3: Call check_logp()

```python
check_logp(pm.HyperGeometric, Nat, {'N': N_domain, 'k': k_domain, 'n': n_domain}, lambda value, N, k, n: st.hypergeom.logpmf(value, N, k, n))
```

### Step 4: Call check_logcdf()

```python
check_logcdf(pm.HyperGeometric, Nat, {'N': N_domain, 'k': k_domain, 'n': n_domain}, modified_scipy_hypergeom_logcdf)
```

### Step 5: Call check_selfconsistency_discrete_logcdf()

```python
check_selfconsistency_discrete_logcdf(pm.HyperGeometric, Nat, {'N': N_domain, 'k': k_domain, 'n': n_domain})
```

### Step 6: Assign original_res = st.hypergeom.logcdf(...)

```python
original_res = st.hypergeom.logcdf(value, N, k, n)
```

### Step 7: Assign pmfs = st.hypergeom.logpmf(...)

```python
pmfs = st.hypergeom.logpmf(np.arange(value + 1), N, k, n)
```

### Step 8: Assign original_res = value

```python
original_res = np.nan
```


## Complete Example

```python
# Workflow
def modified_scipy_hypergeom_logcdf(value, N, k, n):
    original_res = st.hypergeom.logcdf(value, N, k, n)
    if not np.isnan(original_res):
        pmfs = st.hypergeom.logpmf(np.arange(value + 1), N, k, n)
        if np.all(np.isnan(pmfs)):
            original_res = np.nan
    return original_res
N_domain = Domain([0, 10, 20, 30, np.inf], dtype='int64')
n_domain = k_domain = Domain([0, 1, 2, 3, np.inf], dtype='int64')
check_logp(pm.HyperGeometric, Nat, {'N': N_domain, 'k': k_domain, 'n': n_domain}, lambda value, N, k, n: st.hypergeom.logpmf(value, N, k, n))
check_logcdf(pm.HyperGeometric, Nat, {'N': N_domain, 'k': k_domain, 'n': n_domain}, modified_scipy_hypergeom_logcdf)
check_selfconsistency_discrete_logcdf(pm.HyperGeometric, Nat, {'N': N_domain, 'k': k_domain, 'n': n_domain})
```

## Next Steps


---

*Source: test_discrete.py:158 | Complexity: Advanced | Last updated: 2026-05-18*