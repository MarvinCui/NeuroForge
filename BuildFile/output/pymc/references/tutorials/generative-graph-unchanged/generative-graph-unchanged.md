# How To: Generative Graph Unchanged

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test generative graph unchanged

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.raise_op`
- `pytensor.scan.utils`
- `scipy`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.scan`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign rng = pytensor.shared(...)

```python
rng = pytensor.shared(np.random.default_rng())
```

**Verification:**
```python
assert before == after
```

### Step 2: Assign unknown = pytensor.scan(...)

```python
xs, _eps, _rng = pytensor.scan(step, outputs_info=[None, pt.ones(()), rng], n_steps=5, return_updates=False)
```

### Step 3: Assign before = xs.dprint(...)

```python
before = xs.dprint(file='str')
```

### Step 4: Assign xs_value = np.ones(...)

```python
xs_value = np.ones(5)
```

### Step 5: Assign expected_logp = stats.norm.logpdf(...)

```python
expected_logp = stats.norm.logpdf(xs_value, 0, 1)
```

### Step 6: Assign after = xs.dprint(...)

```python
after = xs.dprint(file='str')
```

**Verification:**
```python
assert before == after
```

### Step 7: Assign unknown = value

```python
next_rng, x = pt.random.normal(0, eps_tm1, rng=rng).owner.outputs
```

### Step 8: Assign eps_t = value

```python
eps_t = x - 0
```

### Step 9: Assign xs_logp = logp(...)

```python
xs_logp = logp(xs, xs_value)
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(xs_logp.eval(), expected_logp)
```


## Complete Example

```python
# Workflow
rng = pytensor.shared(np.random.default_rng())

def step(eps_tm1, rng):
    next_rng, x = pt.random.normal(0, eps_tm1, rng=rng).owner.outputs
    eps_t = x - 0
    return (x, eps_t, next_rng)
xs, _eps, _rng = pytensor.scan(step, outputs_info=[None, pt.ones(()), rng], n_steps=5, return_updates=False)
before = xs.dprint(file='str')
xs_value = np.ones(5)
expected_logp = stats.norm.logpdf(xs_value, 0, 1)
for i in range(2):
    xs_logp = logp(xs, xs_value)
    np.testing.assert_allclose(xs_logp.eval(), expected_logp)
after = xs.dprint(file='str')
assert before == after
```

## Next Steps


---

*Source: test_scan.py:566 | Complexity: Advanced | Last updated: 2026-05-18*