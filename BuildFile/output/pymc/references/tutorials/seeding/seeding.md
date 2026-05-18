# How To: Seeding

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test seeding

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `re`
- `warnings`
- `collections.abc`
- `typing`
- `unittest`
- `jax`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc.exceptions`
- `pymc.sampling.jax`

**Setup Required:**
```python
# Fixtures: chains, random_seed, sampler
```

## Step-by-Step Guide

### Step 1: Assign sample_kwargs = value

```python
sample_kwargs = {'tune': 100, 'draws': 5, 'chains': chains, 'random_seed': random_seed}
```

**Verification:**
```python
assert not all_equal
```

### Step 2: Assign all_equal = np.all(...)

```python
all_equal = np.all(result1.posterior['x'] == result2.posterior['x'])
```

**Verification:**
```python
assert all_equal
```

### Step 3: Call pm.Normal()

```python
pm.Normal('x', mu=0, sigma=1)
```

**Verification:**
```python
assert np.all(result1.posterior['x'].sel(chain=0) != result1.posterior['x'].sel(chain=1))
```

### Step 4: Assign result1 = sampler(...)

```python
result1 = sampler(**sample_kwargs)
```

**Verification:**
```python
assert np.all(result2.posterior['x'].sel(chain=0) != result2.posterior['x'].sel(chain=1))
```

### Step 5: Assign result2 = sampler(...)

```python
result2 = sampler(**sample_kwargs)
```

**Verification:**
```python
assert not all_equal
```


## Complete Example

```python
# Setup
# Fixtures: chains, random_seed, sampler

# Workflow
sample_kwargs = {'tune': 100, 'draws': 5, 'chains': chains, 'random_seed': random_seed}
with pm.Model() as m:
    pm.Normal('x', mu=0, sigma=1)
    result1 = sampler(**sample_kwargs)
    result2 = sampler(**sample_kwargs)
all_equal = np.all(result1.posterior['x'] == result2.posterior['x'])
if random_seed is None:
    assert not all_equal
else:
    assert all_equal
if chains > 1:
    assert np.all(result1.posterior['x'].sel(chain=0) != result1.posterior['x'].sel(chain=1))
    assert np.all(result2.posterior['x'].sel(chain=0) != result2.posterior['x'].sel(chain=1))
```

## Next Steps


---

*Source: test_jax.py:369 | Complexity: Intermediate | Last updated: 2026-05-18*