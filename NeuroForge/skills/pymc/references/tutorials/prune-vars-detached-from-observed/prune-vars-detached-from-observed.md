# How To: Prune Vars Detached From Observed

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test prune vars detached from observed

## Prerequisites

**Required Modules:**
- `numpy`
- `pymc`
- `pymc.model.transform.basic`


## Step-by-Step Guide

### Step 1: Assign pruned_m = prune_vars_detached_from_observed(...)

```python
pruned_m = prune_vars_detached_from_observed(m)
```

**Verification:**
```python
assert set(m.named_vars.keys()) == {'obs_data', 'a0', 'a1', 'a2', 'obs', 'd0', 'd1'}
```

### Step 2: Assign obs_data = pm.Data(...)

```python
obs_data = pm.Data('obs_data', 0)
```

**Verification:**
```python
assert set(pruned_m.named_vars.keys()) == {'obs_data', 'a0', 'a1', 'a2', 'obs'}
```

### Step 3: Assign a0 = pm.Data(...)

```python
a0 = pm.Data('a0', 0)
```

### Step 4: Assign a1 = pm.Normal(...)

```python
a1 = pm.Normal('a1', a0)
```

### Step 5: Assign a2 = pm.Normal(...)

```python
a2 = pm.Normal('a2', a1)
```

### Step 6: Call pm.Normal()

```python
pm.Normal('obs', a2, observed=obs_data)
```

### Step 7: Assign d0 = pm.Data(...)

```python
d0 = pm.Data('d0', 0)
```

### Step 8: Assign d1 = pm.Normal(...)

```python
d1 = pm.Normal('d1', d0)
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    obs_data = pm.Data('obs_data', 0)
    a0 = pm.Data('a0', 0)
    a1 = pm.Normal('a1', a0)
    a2 = pm.Normal('a2', a1)
    pm.Normal('obs', a2, observed=obs_data)
    d0 = pm.Data('d0', 0)
    d1 = pm.Normal('d1', d0)
assert set(m.named_vars.keys()) == {'obs_data', 'a0', 'a1', 'a2', 'obs', 'd0', 'd1'}
pruned_m = prune_vars_detached_from_observed(m)
assert set(pruned_m.named_vars.keys()) == {'obs_data', 'a0', 'a1', 'a2', 'obs'}
```

## Next Steps


---

*Source: test_basic.py:21 | Complexity: Advanced | Last updated: 2026-05-18*