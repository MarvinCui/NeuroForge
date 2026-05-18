# How To: Drop Warning Stat

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate from_dict: test drop warning stat

## Prerequisites

**Required Modules:**
- `re`
- `arviz`
- `numpy`
- `pytest`
- `xarray`
- `cachetools`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.util`


## Step-by-Step Guide

### Step 1: Assign idata = arviz.from_dict(...)

```python
idata = arviz.from_dict({'sample_stats': {'a': np.ones((2, 5, 4)), 'warning': np.ones((2, 5, 3), dtype=object)}, 'warmup_sample_stats': {'a': np.ones((2, 5, 4)), 'warning': np.ones((2, 5, 3), dtype=object)}}, attrs={'/': {'version': '0.1.2'}}, coords={'adim': [0, 1, None, 3], 'warning_dim_0': list('ABC')}, dims={'a': ['adim'], 'warning': ['warning_dim_0']}, save_warmup=True)
```


## Complete Example

```python
# Workflow
idata = arviz.from_dict({'sample_stats': {'a': np.ones((2, 5, 4)), 'warning': np.ones((2, 5, 3), dtype=object)}, 'warmup_sample_stats': {'a': np.ones((2, 5, 4)), 'warning': np.ones((2, 5, 3), dtype=object)}}, attrs={'/': {'version': '0.1.2'}}, coords={'adim': [0, 1, None, 3], 'warning_dim_0': list('ABC')}, dims={'a': ['adim'], 'warning': ['warning_dim_0']}, save_warmup=True)
```

## Next Steps


---

*Source: test_util.py:159 | Complexity: Beginner | Last updated: 2026-05-18*