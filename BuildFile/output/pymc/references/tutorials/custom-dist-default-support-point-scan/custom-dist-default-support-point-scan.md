# How To: Custom Dist Default Support Point Scan

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test custom dist default support point scan

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

### Step 1: Call assert_support_point_is_expected()

```python
assert_support_point_is_expected(model, np.array([-3, -2]))
```

**Verification:**
```python
assert_support_point_is_expected(model, np.array([-3, -2]))
```

### Step 2: Assign x = Uniform.dist(...)

```python
x = Uniform.dist(left, right, rng=rng)
```

### Step 3: Assign x_update = collect_default_updates(...)

```python
x_update = collect_default_updates([x], must_be_shared=False)
```

### Step 4: Assign rng = pytensor.shared(...)

```python
rng = pytensor.shared(np.random.default_rng())
```

### Step 5: Assign unknown = scan(...)

```python
xs, next_rng = scan(fn=scan_step, sequences=[pt.as_tensor_variable(np.array([-4, -3])), pt.as_tensor_variable(np.array([-2, -1]))], outputs_info=[None, rng], name='xs', return_updates=False)
```

### Step 6: Call CustomDist()

```python
CustomDist('x', dist=dist)
```


## Complete Example

```python
# Workflow
def scan_step(left, right, rng):
    x = Uniform.dist(left, right, rng=rng)
    x_update = collect_default_updates([x], must_be_shared=False)
    return (x, x_update[rng])

def dist(size):
    rng = pytensor.shared(np.random.default_rng())
    xs, next_rng = scan(fn=scan_step, sequences=[pt.as_tensor_variable(np.array([-4, -3])), pt.as_tensor_variable(np.array([-2, -1]))], outputs_info=[None, rng], name='xs', return_updates=False)
    return xs
with Model() as model:
    CustomDist('x', dist=dist)
assert_support_point_is_expected(model, np.array([-3, -2]))
```

## Next Steps


---

*Source: test_custom.py:363 | Complexity: Intermediate | Last updated: 2026-05-18*