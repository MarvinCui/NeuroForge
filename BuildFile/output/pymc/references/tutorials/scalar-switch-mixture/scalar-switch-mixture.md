# How To: Scalar Switch Mixture

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test scalar switch mixture

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
assert Z1_rv.eval({I_rv: 0}) > 5
```

### Step 2: Assign X_rv = srng.normal(...)

```python
X_rv = srng.normal(-10.0, 0.1, name='X')
```

**Verification:**
```python
assert Z1_rv.eval({I_rv: 1}) < -5
```

### Step 3: Assign Y_rv = srng.normal(...)

```python
Y_rv = srng.normal(10.0, 0.1, name='Y')
```

**Verification:**
```python
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableSwitchMixture)
```

### Step 4: Assign I_rv = srng.bernoulli(...)

```python
I_rv = srng.bernoulli(0.5, name='I')
```

**Verification:**
```python
assert Z2_rv.eval({I_rv: 0}) > 5
```

### Step 5: Assign i_vv = I_rv.clone(...)

```python
i_vv = I_rv.clone()
```

**Verification:**
```python
assert Z2_rv.eval({I_rv: 1}) < -5
```

### Step 6: Assign i_vv.name = 'i'

```python
i_vv.name = 'i'
```

### Step 7: Assign Z1_rv = pt.switch(...)

```python
Z1_rv = pt.switch(I_rv, X_rv, Y_rv)
```

### Step 8: Assign Z1_rv.name = 'Z1'

```python
Z1_rv.name = 'Z1'
```

**Verification:**
```python
assert Z1_rv.eval({I_rv: 0}) > 5
```

### Step 9: Assign z_vv = Z1_rv.clone(...)

```python
z_vv = Z1_rv.clone()
```

### Step 10: Assign z_vv.name = 'z1'

```python
z_vv.name = 'z1'
```

### Step 11: Assign fgraph = construct_ir_fgraph(...)

```python
fgraph = construct_ir_fgraph({Z1_rv: z_vv, I_rv: i_vv})
```

**Verification:**
```python
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableSwitchMixture)
```

### Step 12: Assign Z2_rv = value

```python
Z2_rv = pt.stack((Y_rv, X_rv))[I_rv]
```

**Verification:**
```python
assert Z2_rv.eval({I_rv: 0}) > 5
```

### Step 13: Assign z1_logp = conditional_logp(...)

```python
z1_logp = conditional_logp({Z1_rv: z_vv, I_rv: i_vv})
```

### Step 14: Assign z2_logp = conditional_logp(...)

```python
z2_logp = conditional_logp({Z2_rv: z_vv, I_rv: i_vv})
```

### Step 15: Assign z1_logp_combined = pt.sum(...)

```python
z1_logp_combined = pt.sum([pt.sum(factor) for factor in z1_logp.values()])
```

### Step 16: Assign z2_logp_combined = pt.sum(...)

```python
z2_logp_combined = pt.sum([pt.sum(factor) for factor in z2_logp.values()])
```

### Step 17: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(0.69049938, z1_logp_combined.eval({z_vv: -10, i_vv: 1}))
```

### Step 18: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(0.69049938, z2_logp_combined.eval({z_vv: -10, i_vv: 1}))
```


## Complete Example

```python
# Workflow
srng = pt.random.RandomStream(29833)
X_rv = srng.normal(-10.0, 0.1, name='X')
Y_rv = srng.normal(10.0, 0.1, name='Y')
I_rv = srng.bernoulli(0.5, name='I')
i_vv = I_rv.clone()
i_vv.name = 'i'
Z1_rv = pt.switch(I_rv, X_rv, Y_rv)
Z1_rv.name = 'Z1'
assert Z1_rv.eval({I_rv: 0}) > 5
assert Z1_rv.eval({I_rv: 1}) < -5
z_vv = Z1_rv.clone()
z_vv.name = 'z1'
fgraph = construct_ir_fgraph({Z1_rv: z_vv, I_rv: i_vv})
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableSwitchMixture)
Z2_rv = pt.stack((Y_rv, X_rv))[I_rv]
assert Z2_rv.eval({I_rv: 0}) > 5
assert Z2_rv.eval({I_rv: 1}) < -5
z1_logp = conditional_logp({Z1_rv: z_vv, I_rv: i_vv})
z2_logp = conditional_logp({Z2_rv: z_vv, I_rv: i_vv})
z1_logp_combined = pt.sum([pt.sum(factor) for factor in z1_logp.values()])
z2_logp_combined = pt.sum([pt.sum(factor) for factor in z2_logp.values()])
np.testing.assert_almost_equal(0.69049938, z1_logp_combined.eval({z_vv: -10, i_vv: 1}))
np.testing.assert_almost_equal(0.69049938, z2_logp_combined.eval({z_vv: -10, i_vv: 1}))
```

## Next Steps


---

*Source: test_mixture.py:848 | Complexity: Advanced | Last updated: 2026-05-18*