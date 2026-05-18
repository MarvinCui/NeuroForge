# How To: Mcmc Draws Stat Shows Completed Count

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mcmc draws stat shows completed count

## Prerequisites

**Required Modules:**
- `unittest.mock`
- `pytest`
- `pymc`
- `pymc.progress_bar`
- `pymc.smc.kernels`
- `pymc.step_methods`


## Step-by-Step Guide

### Step 1: Assign manager = MCMCProgressBarManager(...)

```python
manager = MCMCProgressBarManager(step_method=step, chains=1, draws=10, tune=5, progressbar=True)
```

**Verification:**
```python
assert _get_task(manager).fields['draw'] == 1
```

### Step 2: Call pm.Normal()

```python
pm.Normal('x')
```

**Verification:**
```python
assert _get_task(manager).fields['draw'] == 15
```

### Step 3: Assign step = pm.NUTS(...)

```python
step = pm.NUTS()
```

### Step 4: Call manager.update()

```python
manager.update(chain_idx=0, is_last=False, draw=0, tuning=True, stats=NUTS_DUMMY_STATS)
```

**Verification:**
```python
assert _get_task(manager).fields['draw'] == 1
```

### Step 5: Call manager.update()

```python
manager.update(chain_idx=0, is_last=i == 14, draw=i, tuning=i < 5, stats=NUTS_DUMMY_STATS)
```


## Complete Example

```python
# Workflow
with pm.Model():
    pm.Normal('x')
    step = pm.NUTS()
manager = MCMCProgressBarManager(step_method=step, chains=1, draws=10, tune=5, progressbar=True)
with manager:
    manager.update(chain_idx=0, is_last=False, draw=0, tuning=True, stats=NUTS_DUMMY_STATS)
    assert _get_task(manager).fields['draw'] == 1
    for i in range(1, 15):
        manager.update(chain_idx=0, is_last=i == 14, draw=i, tuning=i < 5, stats=NUTS_DUMMY_STATS)
    assert _get_task(manager).fields['draw'] == 15
```

## Next Steps


---

*Source: test_manager.py:103 | Complexity: Intermediate | Last updated: 2026-05-18*