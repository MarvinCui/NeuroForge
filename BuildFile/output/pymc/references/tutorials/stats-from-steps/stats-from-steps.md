# How To: Stats From Steps

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test stats from steps

## Prerequisites

**Required Modules:**
- `pytensor`
- `pytest`
- `pymc`
- `pymc.step_methods`
- `pymc.step_methods.compound`
- `pymc.testing`
- `tests.helpers`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign sds = get_stats_dtypes_shapes_from_steps(...)

```python
sds = get_stats_dtypes_shapes_from_steps([s1, s2])
```

**Verification:**
```python
assert pm.NUTS.stats_dtypes == []
```

### Step 2: Assign s1 = pm.NUTS(...)

```python
s1 = pm.NUTS(pm.Normal('n'))
```

**Verification:**
```python
assert pm.Metropolis.stats_dtypes == []
```

### Step 3: Assign s2 = pm.Metropolis(...)

```python
s2 = pm.Metropolis(pm.Bernoulli('b', 0.5))
```

**Verification:**
```python
assert 'sampler_0__step_size' in sds
```

### Step 4: Assign cs = CompoundStep(...)

```python
cs = CompoundStep([s1, s2])
```

**Verification:**
```python
assert 'sampler_1__accepted' in sds
```


## Complete Example

```python
# Workflow
with pm.Model():
    s1 = pm.NUTS(pm.Normal('n'))
    s2 = pm.Metropolis(pm.Bernoulli('b', 0.5))
    cs = CompoundStep([s1, s2])
assert pm.NUTS.stats_dtypes == []
assert pm.Metropolis.stats_dtypes == []
sds = get_stats_dtypes_shapes_from_steps([s1, s2])
assert 'sampler_0__step_size' in sds
assert 'sampler_1__accepted' in sds
assert len(cs.stats_dtypes) == 2
assert cs.stats_dtypes_shapes == sds
```

## Next Steps


---

*Source: test_compound.py:139 | Complexity: Intermediate | Last updated: 2026-05-18*