# How To: Scalar Clipped Mixture

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test scalar clipped mixture

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign x = pt.clip(...)

```python
x = pt.clip(pt.random.normal(loc=1), 0.5, 1.5)
```

**Verification:**
```python
assert logp_fn(0, 0.4) == -np.inf
```

### Step 2: Assign x.name = 'x'

```python
x.name = 'x'
```

**Verification:**
```python
assert np.isclose(logp_fn(0, 0.5), st.norm.logcdf(0.5, 1) + np.log(0.6))
```

### Step 3: Assign y = pt.random.beta(...)

```python
y = pt.random.beta(1, 2, name='y')
```

**Verification:**
```python
assert np.isclose(logp_fn(0, 1.3), st.norm.logpdf(1.3, 1) + np.log(0.6))
```

### Step 4: Assign comps = pt.stack(...)

```python
comps = pt.stack([x, y])
```

**Verification:**
```python
assert np.isclose(logp_fn(1, 0.4), st.beta.logpdf(0.4, 1, 2) + np.log(0.4))
```

### Step 5: Assign comps.name = 'comps'

```python
comps.name = 'comps'
```

### Step 6: Assign idxs = pt.random.bernoulli(...)

```python
idxs = pt.random.bernoulli(0.4, name='idxs')
```

### Step 7: Assign mix = value

```python
mix = comps[idxs]
```

### Step 8: Assign mix.name = 'mix'

```python
mix.name = 'mix'
```

### Step 9: Assign mix_vv = mix.clone(...)

```python
mix_vv = mix.clone()
```

### Step 10: Assign mix_vv.name = 'mix_val'

```python
mix_vv.name = 'mix_val'
```

### Step 11: Assign idxs_vv = idxs.clone(...)

```python
idxs_vv = idxs.clone()
```

### Step 12: Assign idxs_vv.name = 'idxs_val'

```python
idxs_vv.name = 'idxs_val'
```

### Step 13: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({idxs: idxs_vv, mix: mix_vv})
```

### Step 14: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 15: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([idxs_vv, mix_vv], logp_combined)
```

**Verification:**
```python
assert logp_fn(0, 0.4) == -np.inf
```


## Complete Example

```python
# Workflow
x = pt.clip(pt.random.normal(loc=1), 0.5, 1.5)
x.name = 'x'
y = pt.random.beta(1, 2, name='y')
comps = pt.stack([x, y])
comps.name = 'comps'
idxs = pt.random.bernoulli(0.4, name='idxs')
mix = comps[idxs]
mix.name = 'mix'
mix_vv = mix.clone()
mix_vv.name = 'mix_val'
idxs_vv = idxs.clone()
idxs_vv.name = 'idxs_val'
logp = conditional_logp({idxs: idxs_vv, mix: mix_vv})
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
logp_fn = pytensor.function([idxs_vv, mix_vv], logp_combined)
assert logp_fn(0, 0.4) == -np.inf
assert np.isclose(logp_fn(0, 0.5), st.norm.logcdf(0.5, 1) + np.log(0.6))
assert np.isclose(logp_fn(0, 1.3), st.norm.logpdf(1.3, 1) + np.log(0.6))
assert np.isclose(logp_fn(1, 0.4), st.beta.logpdf(0.4, 1, 2) + np.log(0.4))
```

## Next Steps


---

*Source: test_composite_logprob.py:50 | Complexity: Advanced | Last updated: 2026-05-18*