# How To: Mixture Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Make sure that non-`RandomVariable` `MeasurableOp` variables can be transformed.

This test is specific to `MixtureRV`, which is derived from an `OpFromGraph`.

## Prerequisites

**Required Modules:**
- `gc`
- `operator`
- `numpy`
- `pytensor`
- `pytest`
- `scipy`
- `numdifftools`
- `pytensor`
- `pytensor`
- `pytensor.compile.builders`
- `pytensor.graph`
- `pytensor.graph.basic`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob`
- `pymc.logprob.abstract`
- `pymc.logprob.transform_value`
- `pymc.logprob.transforms`
- `pymc.testing`
- `tests.logprob.test_transforms`
- `pymc.model.transform.optimization`


## Step-by-Step Guide

### Step 1: 'Make sure that non-`RandomVariable` `MeasurableOp` variables can be transformed.\n\n    This test is specific to `MixtureRV`, which is derived from an `OpFromGraph`.\n    '

```python
'Make sure that non-`RandomVariable` `MeasurableOp` variables can be transformed.\n\n    This test is specific to `MixtureRV`, which is derived from an `OpFromGraph`.\n    '
```

**Verification:**
```python
assert equal_computations([logp_nt], [logp_trans_combined])
```

### Step 2: Assign unknown = pt.random.bernoulli(...)

```python
_, I_rv = pt.random.bernoulli(0.5, name='I', rng=pt.random.shared_rng(seed=None), return_next_rng=True)
```

### Step 3: Assign unknown = pt.random.beta(...)

```python
_, Y_1_rv = pt.random.beta(100, 1, name='Y_1', rng=pt.random.shared_rng(seed=None), return_next_rng=True)
```

### Step 4: Assign unknown = pt.random.beta(...)

```python
_, Y_2_rv = pt.random.beta(1, 100, name='Y_2', rng=pt.random.shared_rng(seed=None), return_next_rng=True)
```

### Step 5: Assign Y_rv = value

```python
Y_rv = pt.stack([Y_1_rv, Y_2_rv])[I_rv]
```

### Step 6: Assign Y_rv.name = 'Y'

```python
Y_rv.name = 'Y'
```

### Step 7: Assign i_vv = I_rv.clone(...)

```python
i_vv = I_rv.clone()
```

### Step 8: Assign i_vv.name = 'i'

```python
i_vv.name = 'i'
```

### Step 9: Assign y_vv = Y_rv.clone(...)

```python
y_vv = Y_rv.clone()
```

### Step 10: Assign y_vv.name = 'y'

```python
y_vv.name = 'y'
```

### Step 11: Assign logp_no_trans = conditional_logp(...)

```python
logp_no_trans = conditional_logp({Y_rv: y_vv, I_rv: i_vv})
```

### Step 12: Assign logp_no_trans_comb = pt.sum(...)

```python
logp_no_trans_comb = pt.sum([pt.sum(factor) for factor in logp_no_trans.values()])
```

### Step 13: Assign transform_rewrite = TransformValuesRewrite(...)

```python
transform_rewrite = TransformValuesRewrite({y_vv: LogTransform()})
```

### Step 14: Assign logp_trans = conditional_logp(...)

```python
logp_trans = conditional_logp({Y_rv: y_vv, I_rv: i_vv}, extra_rewrites=transform_rewrite, use_jacobian=False)
```

### Step 15: Assign logp_trans_combined = pt.sum(...)

```python
logp_trans_combined = pt.sum([pt.sum(factor) for factor in logp_trans.values()])
```

### Step 16: Assign logp_nt_fg = FunctionGraph(...)

```python
logp_nt_fg = FunctionGraph(outputs=[logp_no_trans_comb], clone=False)
```

### Step 17: Assign y_trans = pt.exp(...)

```python
y_trans = pt.exp(y_vv)
```

### Step 18: Assign y_trans.name = 'y_log'

```python
y_trans.name = 'y_log'
```

### Step 19: Call logp_nt_fg.replace()

```python
logp_nt_fg.replace(y_vv, y_trans)
```

### Step 20: Assign logp_nt = value

```python
logp_nt = logp_nt_fg.outputs[0]
```

**Verification:**
```python
assert equal_computations([logp_nt], [logp_trans_combined])
```


## Complete Example

```python
# Workflow
'Make sure that non-`RandomVariable` `MeasurableOp` variables can be transformed.\n\n    This test is specific to `MixtureRV`, which is derived from an `OpFromGraph`.\n    '
_, I_rv = pt.random.bernoulli(0.5, name='I', rng=pt.random.shared_rng(seed=None), return_next_rng=True)
_, Y_1_rv = pt.random.beta(100, 1, name='Y_1', rng=pt.random.shared_rng(seed=None), return_next_rng=True)
_, Y_2_rv = pt.random.beta(1, 100, name='Y_2', rng=pt.random.shared_rng(seed=None), return_next_rng=True)
Y_rv = pt.stack([Y_1_rv, Y_2_rv])[I_rv]
Y_rv.name = 'Y'
i_vv = I_rv.clone()
i_vv.name = 'i'
y_vv = Y_rv.clone()
y_vv.name = 'y'
logp_no_trans = conditional_logp({Y_rv: y_vv, I_rv: i_vv})
logp_no_trans_comb = pt.sum([pt.sum(factor) for factor in logp_no_trans.values()])
transform_rewrite = TransformValuesRewrite({y_vv: LogTransform()})
logp_trans = conditional_logp({Y_rv: y_vv, I_rv: i_vv}, extra_rewrites=transform_rewrite, use_jacobian=False)
logp_trans_combined = pt.sum([pt.sum(factor) for factor in logp_trans.values()])
logp_nt_fg = FunctionGraph(outputs=[logp_no_trans_comb], clone=False)
y_trans = pt.exp(y_vv)
y_trans.name = 'y_log'
logp_nt_fg.replace(y_vv, y_trans)
logp_nt = logp_nt_fg.outputs[0]
assert equal_computations([logp_nt], [logp_trans_combined])
```

## Next Steps


---

*Source: test_transform_value.py:476 | Complexity: Advanced | Last updated: 2026-05-18*