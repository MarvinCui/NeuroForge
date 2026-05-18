# How To: No Change Inplace

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test no change inplace

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.graph.replace`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign before = clone_replace(...)

```python
before = clone_replace(m.free_RVs)
```

**Verification:**
```python
assert equal_computations(before, after)
```

### Step 2: Call replace_rvs_by_values()

```python
replace_rvs_by_values(m.potentials, rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
```

### Step 3: Assign after = clone_replace(...)

```python
after = clone_replace(m.free_RVs)
```

**Verification:**
```python
assert equal_computations(before, after)
```

### Step 4: Assign one = pm.LogNormal(...)

```python
one = pm.LogNormal('one', mu=0)
```

### Step 5: Assign two = pm.LogNormal(...)

```python
two = pm.LogNormal('two', mu=pt.log(one))
```

### Step 6: Call pm.Potential()

```python
pm.Potential('two_pot', two)
```

### Step 7: Call pm.Potential()

```python
pm.Potential('one_pot', one)
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    one = pm.LogNormal('one', mu=0)
    two = pm.LogNormal('two', mu=pt.log(one))
    pm.Potential('two_pot', two)
    pm.Potential('one_pot', one)
before = clone_replace(m.free_RVs)
replace_rvs_by_values(m.potentials, rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
after = clone_replace(m.free_RVs)
assert equal_computations(before, after)
```

## Next Steps


---

*Source: test_utils.py:186 | Complexity: Intermediate | Last updated: 2026-05-18*