# How To: Tuning Reset

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Re-use of the step method instance with cores=1 must not leak tuning information between chains.

## Prerequisites

**Required Modules:**
- `warnings`
- `arviz`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytest`
- `pytensor.compile.mode`
- `pymc`
- `pymc.step_methods.metropolis`
- `pymc.step_methods.state`
- `pymc.testing`
- `tests`
- `tests.helpers`
- `tests.models`


## Step-by-Step Guide

### Step 1: 'Re-use of the step method instance with cores=1 must not leak tuning information between chains.'

```python
'Re-use of the step method instance with cores=1 must not leak tuning information between chains.'
```

**Verification:**
```python
assert warmup[0] == 0.002
```

### Step 2: Assign D = 3

```python
D = 3
```

**Verification:**
```python
assert warmup[-1] != 0.002
```

### Step 3: Call pm.Normal()

```python
pm.Normal('n', 0, 2, size=(D,))
```

**Verification:**
```python
assert var_start < 0.1 * var_end
```

### Step 4: Assign idata = pm.sample(...)

```python
idata = pm.sample(tune=1000, draws=500, step=DEMetropolisZ(tune='scaling', scaling=0.002, rng=SEED), cores=1, chains=3, discard_tuned_samples=False, random_seed=1)
```

### Step 5: Assign warmup = value

```python
warmup = idata.warmup_sample_stats['scaling'].sel(chain=c).values
```

**Verification:**
```python
assert warmup[0] == 0.002
```

### Step 6: Assign samples = value

```python
samples = idata.warmup_posterior['n'].sel(chain=c).values
```

### Step 7: Assign var_start = np.var(...)

```python
var_start = np.var(samples[:50, d])
```

### Step 8: Assign var_end = np.var(...)

```python
var_end = np.var(samples[-100:, d])
```

**Verification:**
```python
assert var_start < 0.1 * var_end
```


## Complete Example

```python
# Workflow
'Re-use of the step method instance with cores=1 must not leak tuning information between chains.'
with pm.Model() as pmodel:
    D = 3
    pm.Normal('n', 0, 2, size=(D,))
    idata = pm.sample(tune=1000, draws=500, step=DEMetropolisZ(tune='scaling', scaling=0.002, rng=SEED), cores=1, chains=3, discard_tuned_samples=False, random_seed=1)
for c in idata.posterior.chain:
    warmup = idata.warmup_sample_stats['scaling'].sel(chain=c).values
    assert warmup[0] == 0.002
    assert warmup[-1] != 0.002
    samples = idata.warmup_posterior['n'].sel(chain=c).values
    for d in range(D):
        var_start = np.var(samples[:50, d])
        var_end = np.var(samples[-100:, d])
        assert var_start < 0.1 * var_end
```

## Next Steps


---

*Source: test_metropolis.py:230 | Complexity: Advanced | Last updated: 2026-05-18*