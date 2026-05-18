# How To: Scan Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that Scan valued variables can be transformed

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

### Step 1: 'Test that Scan valued variables can be transformed'

```python
'Test that Scan valued variables can be transformed'
```

### Step 2: Assign unknown = value

```python
rng, init = pt.random.beta(1, 1, name='init').owner.outputs
```

### Step 3: Assign init_vv = init.clone(...)

```python
init_vv = init.clone()
```

### Step 4: Assign unknown = scan(...)

```python
innov, _next_rng = scan(fn=scan_step, outputs_info=[init, rng], n_steps=4, return_updates=False)
```

### Step 5: Assign innov.name = 'innov'

```python
innov.name = 'innov'
```

### Step 6: Assign innov_vv = innov.clone(...)

```python
innov_vv = innov.clone()
```

### Step 7: Assign tr = TransformValuesRewrite(...)

```python
tr = TransformValuesRewrite({init_vv: LogOddsTransform(), innov_vv: LogOddsTransform()})
```

### Step 8: Assign logp = value

```python
logp = conditional_logp({init: init_vv, innov: innov_vv}, extra_rewrites=tr, use_jacobian=True)[innov_vv]
```

### Step 9: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([init_vv, innov_vv], logp, on_unused_input='ignore')
```

### Step 10: Assign innov = value

```python
innov = []
```

### Step 11: Assign prev_innov = init

```python
prev_innov = init
```

### Step 12: Assign innov = pt.stack(...)

```python
innov = pt.stack(innov)
```

### Step 13: Assign innov.name = 'innov'

```python
innov.name = 'innov'
```

### Step 14: Assign tr = TransformValuesRewrite(...)

```python
tr = TransformValuesRewrite({init_vv: LogOddsTransform(), innov_vv: LogOddsTransform()})
```

### Step 15: Assign ref_logp = value

```python
ref_logp = conditional_logp({init: init_vv, innov: innov_vv}, extra_rewrites=tr, use_jacobian=True)[innov_vv]
```

### Step 16: Assign ref_logp_fn = pytensor.function(...)

```python
ref_logp_fn = pytensor.function([init_vv, innov_vv], ref_logp, on_unused_input='ignore')
```

### Step 17: Assign test_point = value

```python
test_point = {'init': np.array(-0.5), 'innov': np.full((4,), -0.5)}
```

### Step 18: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(**test_point), ref_logp_fn(**test_point))
```

### Step 19: Assign unknown = value

```python
next_rng, next_innov = pt.random.beta(prev_innov * 10, (1 - prev_innov) * 10, rng=prev_rng).owner.outputs
```

### Step 20: Assign next_innov = pt.random.beta(...)

```python
next_innov = pt.random.beta(prev_innov * 10, (1 - prev_innov) * 10, name='innov[i]')
```

### Step 21: Call innov.append()

```python
innov.append(next_innov)
```

### Step 22: Assign prev_innov = next_innov

```python
prev_innov = next_innov
```


## Complete Example

```python
# Workflow
'Test that Scan valued variables can be transformed'
rng, init = pt.random.beta(1, 1, name='init').owner.outputs
init_vv = init.clone()

def scan_step(prev_innov, prev_rng):
    next_rng, next_innov = pt.random.beta(prev_innov * 10, (1 - prev_innov) * 10, rng=prev_rng).owner.outputs
    return (next_innov, next_rng)
innov, _next_rng = scan(fn=scan_step, outputs_info=[init, rng], n_steps=4, return_updates=False)
innov.name = 'innov'
innov_vv = innov.clone()
tr = TransformValuesRewrite({init_vv: LogOddsTransform(), innov_vv: LogOddsTransform()})
logp = conditional_logp({init: init_vv, innov: innov_vv}, extra_rewrites=tr, use_jacobian=True)[innov_vv]
logp_fn = pytensor.function([init_vv, innov_vv], logp, on_unused_input='ignore')
innov = []
prev_innov = init
for i in range(4):
    next_innov = pt.random.beta(prev_innov * 10, (1 - prev_innov) * 10, name='innov[i]')
    innov.append(next_innov)
    prev_innov = next_innov
innov = pt.stack(innov)
innov.name = 'innov'
tr = TransformValuesRewrite({init_vv: LogOddsTransform(), innov_vv: LogOddsTransform()})
ref_logp = conditional_logp({init: init_vv, innov: innov_vv}, extra_rewrites=tr, use_jacobian=True)[innov_vv]
ref_logp_fn = pytensor.function([init_vv, innov_vv], ref_logp, on_unused_input='ignore')
test_point = {'init': np.array(-0.5), 'innov': np.full((4,), -0.5)}
np.testing.assert_allclose(logp_fn(**test_point), ref_logp_fn(**test_point))
```

## Next Steps


---

*Source: test_transform_value.py:527 | Complexity: Advanced | Last updated: 2026-05-18*