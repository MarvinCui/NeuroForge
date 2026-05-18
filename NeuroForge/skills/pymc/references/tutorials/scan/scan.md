# How To: Scan

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test scan

## Prerequisites

**Required Modules:**
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytest`
- `numpy`
- `pytensor`
- `pytensor`
- `pytensor.graph`
- `scipy`
- `pymc.distributions`
- `pymc.distributions.custom`
- `pymc.distributions.distribution`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling`
- `pymc.step_methods`
- `pymc.testing`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign nu = 4

```python
nu = 4
```

**Verification:**
```python
assert x_draw.shape == (steps, batch_size)
```

### Step 2: Assign sigma = 0.7

```python
sigma = 0.7
```

**Verification:**
```python
assert not np.any(draw(x, random_seed=2) == x_draw)
```

### Step 3: Assign steps = 99

```python
steps = 99
```

### Step 4: Assign batch_size = 3

```python
batch_size = 3
```

### Step 5: Assign x = CustomDist.dist(...)

```python
x = CustomDist.dist(nu, sigma, steps, dist=trw, size=batch_size)
```

### Step 6: Assign x_draw = draw(...)

```python
x_draw = draw(x, random_seed=1)
```

**Verification:**
```python
assert x_draw.shape == (steps, batch_size)
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(draw(x, random_seed=1), x_draw)
```

**Verification:**
```python
assert not np.any(draw(x, random_seed=2) == x_draw)
```

### Step 8: Assign ref_dist = RandomWalk.dist(...)

```python
ref_dist = RandomWalk.dist(init_dist=Flat.dist(), innovation_dist=StudentT.dist(nu=nu, sigma=sigma), steps=steps, size=(batch_size,))
```

### Step 9: Assign ref_val = value

```python
ref_val = pt.concatenate([np.zeros((1, batch_size)), x_draw]).T
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp(x, x_draw).eval().sum(0), logp(ref_dist, ref_val).eval())
```

### Step 11: Assign rng = pytensor.shared(...)

```python
rng = pytensor.shared(np.random.default_rng())
```

### Step 12: Assign unknown = scan(...)

```python
xs, _next_rng = scan(fn=step, outputs_info=[pt.zeros(size), rng], non_sequences=[nu, sigma], n_steps=steps, return_updates=False)
```

### Step 13: Assign size = value

```python
size = ()
```

### Step 14: Assign unknown = value

```python
next_rng, x = StudentT.dist(nu=nu, mu=xtm1, sigma=sigma, shape=size, rng=rng).owner.outputs
```


## Complete Example

```python
# Workflow
def trw(nu, sigma, steps, size):
    if rv_size_is_none(size):
        size = ()
    rng = pytensor.shared(np.random.default_rng())

    def step(xtm1, rng, nu, sigma):
        next_rng, x = StudentT.dist(nu=nu, mu=xtm1, sigma=sigma, shape=size, rng=rng).owner.outputs
        return (x, next_rng)
    xs, _next_rng = scan(fn=step, outputs_info=[pt.zeros(size), rng], non_sequences=[nu, sigma], n_steps=steps, return_updates=False)
    return xs
nu = 4
sigma = 0.7
steps = 99
batch_size = 3
x = CustomDist.dist(nu, sigma, steps, dist=trw, size=batch_size)
x_draw = draw(x, random_seed=1)
assert x_draw.shape == (steps, batch_size)
np.testing.assert_allclose(draw(x, random_seed=1), x_draw)
assert not np.any(draw(x, random_seed=2) == x_draw)
ref_dist = RandomWalk.dist(init_dist=Flat.dist(), innovation_dist=StudentT.dist(nu=nu, sigma=sigma), steps=steps, size=(batch_size,))
ref_val = pt.concatenate([np.zeros((1, batch_size)), x_draw]).T
np.testing.assert_allclose(logp(x, x_draw).eval().sum(0), logp(ref_dist, ref_val).eval())
```

## Next Steps


---

*Source: test_custom.py:540 | Complexity: Advanced | Last updated: 2026-05-18*