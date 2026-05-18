# How To: Sampling With Random Generator Matches

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test sampling with random generator matches

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `multiprocessing`
- `os`
- `platform`
- `sys`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.compile.ops`
- `pytensor.tensor.type`
- `pymc`
- `pymc.sampling.parallel`
- `pymc.pytensorf`
- `pymc.step_methods`

**Setup Required:**
```python
# Fixtures: cores
```

## Step-by-Step Guide

### Step 1: Assign kwargs = value

```python
kwargs = {'chains': 2, 'cores': cores, 'tune': 10, 'draws': 10, 'compute_convergence_checks': False, 'progress_bar': False}
```

**Verification:**
```python
assert post1.equals(post2), (post1['x'].mean().item(), post2['x'].mean().item())
```

### Step 2: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 3: Assign post1 = value

```python
post1 = pm.sample(random_seed=np.random.default_rng(42), **kwargs).posterior
```

### Step 4: Assign post2 = value

```python
post2 = pm.sample(random_seed=np.random.default_rng(42), **kwargs).posterior
```


## Complete Example

```python
# Setup
# Fixtures: cores

# Workflow
kwargs = {'chains': 2, 'cores': cores, 'tune': 10, 'draws': 10, 'compute_convergence_checks': False, 'progress_bar': False}
with pm.Model() as m:
    x = pm.Normal('x')
    post1 = pm.sample(random_seed=np.random.default_rng(42), **kwargs).posterior
    post2 = pm.sample(random_seed=np.random.default_rng(42), **kwargs).posterior
assert post1.equals(post2), (post1['x'].mean().item(), post2['x'].mean().item())
```

## Next Steps


---

*Source: test_parallel.py:271 | Complexity: Intermediate | Last updated: 2026-05-18*