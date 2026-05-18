# How To: Mixture With Diracdelta

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mixture with DiracDelta

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.ifelse`
- `pytensor.link.numba`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.shape`
- `pytensor.tensor.subtensor`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.mixture`
- `pymc.logprob.rewriting`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign srng = pt.random.RandomStream(...)

```python
srng = pt.random.RandomStream(29833)
```

**Verification:**
```python
assert m_vv in logp_res
```

### Step 2: Assign X_rv = srng.normal(...)

```python
X_rv = srng.normal(0, 1, name='X')
```

### Step 3: Assign Y_rv = dirac_delta(...)

```python
Y_rv = dirac_delta(0.0)
```

### Step 4: Assign Y_rv.name = 'Y'

```python
Y_rv.name = 'Y'
```

### Step 5: Assign I_rv = srng.categorical(...)

```python
I_rv = srng.categorical([0.5, 0.5], size=1)
```

### Step 6: Assign i_vv = I_rv.clone(...)

```python
i_vv = I_rv.clone()
```

### Step 7: Assign i_vv.name = 'i'

```python
i_vv.name = 'i'
```

### Step 8: Assign M_rv = value

```python
M_rv = pt.stack([X_rv, Y_rv])[I_rv]
```

### Step 9: Assign M_rv.name = 'M'

```python
M_rv.name = 'M'
```

### Step 10: Assign m_vv = M_rv.clone(...)

```python
m_vv = M_rv.clone()
```

### Step 11: Assign m_vv.name = 'm'

```python
m_vv.name = 'm'
```

### Step 12: Assign logp_res = conditional_logp(...)

```python
logp_res = conditional_logp({M_rv: m_vv, I_rv: i_vv})
```

**Verification:**
```python
assert m_vv in logp_res
```


## Complete Example

```python
# Workflow
srng = pt.random.RandomStream(29833)
X_rv = srng.normal(0, 1, name='X')
Y_rv = dirac_delta(0.0)
Y_rv.name = 'Y'
I_rv = srng.categorical([0.5, 0.5], size=1)
i_vv = I_rv.clone()
i_vv.name = 'i'
M_rv = pt.stack([X_rv, Y_rv])[I_rv]
M_rv.name = 'M'
m_vv = M_rv.clone()
m_vv.name = 'm'
logp_res = conditional_logp({M_rv: m_vv, I_rv: i_vv})
assert m_vv in logp_res
```

## Next Steps


---

*Source: test_mixture.py:825 | Complexity: Advanced | Last updated: 2026-05-18*