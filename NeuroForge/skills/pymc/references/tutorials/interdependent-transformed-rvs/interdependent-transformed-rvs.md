# How To: Interdependent Transformed Rvs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test interdependent transformed rvs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.graph.replace`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`

**Setup Required:**
```python
# Fixtures: reversed
```

## Step-by-Step Guide

### Step 1: Assign rvs = value

```python
rvs = [x, y, z, w]
```

**Verification:**
```python
assert_no_rvs(transform_values)
```

### Step 2: Assign transform_values = replace_rvs_by_values(...)

```python
transform_values = replace_rvs_by_values(rvs, rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
```

**Verification:**
```python
assert not any(list(explicit_graph_inputs(rvs)))
```

### Step 3: Call assert_no_rvs()

```python
assert_no_rvs(transform_values)
```

**Verification:**
```python
assert not any(list(explicit_graph_inputs(rvs)))
```

### Step 4: Assign transform_values_fn = m.compile_fn(...)

```python
transform_values_fn = m.compile_fn(transform_values)
```

### Step 5: Assign x_interval_test_value = np.random.rand(...)

```python
x_interval_test_value = np.random.rand()
```

### Step 6: Assign y_interval_test_value = np.random.rand(...)

```python
y_interval_test_value = np.random.rand()
```

### Step 7: Assign z_interval_test_value = np.random.rand(...)

```python
z_interval_test_value = np.random.rand()
```

### Step 8: Assign w_interval_test_value = np.random.rand(...)

```python
w_interval_test_value = np.random.rand()
```

### Step 9: Assign expected_x = transform.backward.eval(...)

```python
expected_x = transform.backward(x_interval_test_value, None, None, None, 0, 1).eval()
```

### Step 10: Assign expected_y = transform.backward.eval(...)

```python
expected_y = transform.backward(y_interval_test_value, None, None, None, 0, pt.exp(expected_x)).eval()
```

### Step 11: Assign expected_z = transform.backward.eval(...)

```python
expected_z = transform.backward(z_interval_test_value, None, None, None, 0, expected_y).eval()
```

### Step 12: Assign expected_w = transform.backward.eval(...)

```python
expected_w = transform.backward(w_interval_test_value, None, None, None, 0, pt.square(expected_z)).eval()
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(transform_values_fn({'x_interval__': x_interval_test_value, 'y_interval__': y_interval_test_value, 'z_interval__': z_interval_test_value, 'w_interval__': w_interval_test_value}), [expected_x, expected_y, expected_z, expected_w])
```

### Step 14: Assign transform = pm.distributions.transforms.Interval(...)

```python
transform = pm.distributions.transforms.Interval(bounds_fn=lambda *inputs: (inputs[-2], inputs[-1]))
```

### Step 15: Assign x = pm.Uniform(...)

```python
x = pm.Uniform('x', lower=0, upper=1, default_transform=transform)
```

### Step 16: Assign y = pm.Uniform(...)

```python
y = pm.Uniform('y', lower=0, upper=pt.exp(x), default_transform=transform)
```

### Step 17: Assign z = pm.Uniform(...)

```python
z = pm.Uniform('z', lower=0, upper=y, default_transform=transform)
```

### Step 18: Assign w = pm.Uniform(...)

```python
w = pm.Uniform('w', lower=0, upper=pt.square(z), default_transform=transform)
```

### Step 19: Assign rvs = value

```python
rvs = rvs[::-1]
```

### Step 20: Assign transform_values = value

```python
transform_values = transform_values[::-1]
```


## Complete Example

```python
# Setup
# Fixtures: reversed

# Workflow
with pm.Model() as m:
    transform = pm.distributions.transforms.Interval(bounds_fn=lambda *inputs: (inputs[-2], inputs[-1]))
    x = pm.Uniform('x', lower=0, upper=1, default_transform=transform)
    y = pm.Uniform('y', lower=0, upper=pt.exp(x), default_transform=transform)
    z = pm.Uniform('z', lower=0, upper=y, default_transform=transform)
    w = pm.Uniform('w', lower=0, upper=pt.square(z), default_transform=transform)
rvs = [x, y, z, w]
if reversed:
    rvs = rvs[::-1]
transform_values = replace_rvs_by_values(rvs, rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
assert_no_rvs(transform_values)
assert not any(list(explicit_graph_inputs(rvs)))
if reversed:
    transform_values = transform_values[::-1]
transform_values_fn = m.compile_fn(transform_values)
x_interval_test_value = np.random.rand()
y_interval_test_value = np.random.rand()
z_interval_test_value = np.random.rand()
w_interval_test_value = np.random.rand()
expected_x = transform.backward(x_interval_test_value, None, None, None, 0, 1).eval()
expected_y = transform.backward(y_interval_test_value, None, None, None, 0, pt.exp(expected_x)).eval()
expected_z = transform.backward(z_interval_test_value, None, None, None, 0, expected_y).eval()
expected_w = transform.backward(w_interval_test_value, None, None, None, 0, pt.square(expected_z)).eval()
np.testing.assert_allclose(transform_values_fn({'x_interval__': x_interval_test_value, 'y_interval__': y_interval_test_value, 'z_interval__': z_interval_test_value, 'w_interval__': w_interval_test_value}), [expected_x, expected_y, expected_z, expected_w])
```

## Next Steps


---

*Source: test_utils.py:210 | Complexity: Advanced | Last updated: 2026-05-18*