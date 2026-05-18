# How To: Nuts Tuning

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nuts tuning

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `pymc`
- `pymc.blocking`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`
- `pymc.step_methods.hmc.base_hmc`
- `tests`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign ss_tuned = value

```python
ss_tuned = idata.warmup_sample_stats['step_size'][0, -1]
```

**Verification:**
```python
assert not step.tune
```

### Step 2: Assign ss_posterior = value

```python
ss_posterior = idata.sample_stats['step_size'][0, :]
```

### Step 3: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(ss_posterior, ss_tuned)
```

### Step 4: Call pm.Normal()

```python
pm.Normal('mu', mu=0, sigma=1)
```

### Step 5: Assign step = pm.NUTS(...)

```python
step = pm.NUTS()
```

### Step 6: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

### Step 7: Assign idata = pm.sample(...)

```python
idata = pm.sample(10, step=step, tune=5, discard_tuned_samples=False, progressbar=False, chains=1)
```


## Complete Example

```python
# Workflow
with pm.Model():
    pm.Normal('mu', mu=0, sigma=1)
    step = pm.NUTS()
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
        idata = pm.sample(10, step=step, tune=5, discard_tuned_samples=False, progressbar=False, chains=1)
assert not step.tune
ss_tuned = idata.warmup_sample_stats['step_size'][0, -1]
ss_posterior = idata.sample_stats['step_size'][0, :]
np.testing.assert_array_equal(ss_posterior, ss_tuned)
```

## Next Steps


---

*Source: test_hmc.py:77 | Complexity: Intermediate | Last updated: 2026-05-18*