# How To: Freeze Dims And Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test freeze dims and data

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc.data`
- `pymc.distributions`
- `pymc.exceptions`
- `pymc.model`
- `pymc.model.transform.optimization`
- `pymc.pytensorf`


## Step-by-Step Guide

### Step 1: Assign unknown = m.logp(...)

```python
x_logp, y_logp = m.logp(sum=False)
```

**Verification:**
```python
assert not isinstance(std, Constant)
```

### Step 2: Assign frozen_m = freeze_dims_and_data(...)

```python
frozen_m = freeze_dims_and_data(m)
```

**Verification:**
```python
assert x.type.shape == (None,)
```

### Step 3: Assign unknown = value

```python
data, x, y = (frozen_m['test_data'], frozen_m['x'], frozen_m['y'])
```

**Verification:**
```python
assert y.type.shape == (None,)
```

### Step 4: Assign unknown = frozen_m.logp(...)

```python
x_logp, y_logp = frozen_m.logp(sum=False)
```

**Verification:**
```python
assert x_logp.type.shape == (None,)
```

### Step 5: Assign std = Data(...)

```python
std = Data('test_data', [1])
```

**Verification:**
```python
assert y_logp.type.shape == (None,)
```

### Step 6: Assign x = HalfNormal(...)

```python
x = HalfNormal('x', std, dims=('test_dim',))
```

**Verification:**
```python
assert isinstance(data, Constant)
```

### Step 7: Assign y = Normal(...)

```python
y = Normal('y', shape=x.shape[0] + 1)
```

**Verification:**
```python
assert x.type.shape == (5,)
```

### Step 8: Call m.set_data()

```python
m.set_data('test_data', values=[2])
```

**Verification:**
```python
assert y.type.shape == (6,)
```

### Step 9: Call m.set_dim()

```python
m.set_dim('test_dim', new_length=6, coord_values=range(6))
```

**Verification:**
```python
assert x_logp.type.shape == (5,)
```

### Step 10: Call frozen_m.set_data()

```python
frozen_m.set_data('test_data', values=[2])
```

**Verification:**
```python
assert y_logp.type.shape == (6,)
```

### Step 11: Call frozen_m.set_dim()

```python
frozen_m.set_dim('test_dim', new_length=6, coord_values=range(6))
```

**Verification:**
```python
assert m['test_data'].get_value() == [2]
```


## Complete Example

```python
# Workflow
with Model(coords={'test_dim': range(5)}) as m:
    std = Data('test_data', [1])
    x = HalfNormal('x', std, dims=('test_dim',))
    y = Normal('y', shape=x.shape[0] + 1)
x_logp, y_logp = m.logp(sum=False)
assert not isinstance(std, Constant)
assert x.type.shape == (None,)
assert y.type.shape == (None,)
assert x_logp.type.shape == (None,)
assert y_logp.type.shape == (None,)
frozen_m = freeze_dims_and_data(m)
data, x, y = (frozen_m['test_data'], frozen_m['x'], frozen_m['y'])
x_logp, y_logp = frozen_m.logp(sum=False)
assert isinstance(data, Constant)
assert x.type.shape == (5,)
assert y.type.shape == (6,)
assert x_logp.type.shape == (5,)
assert y_logp.type.shape == (6,)
with frozen_m:
    with pytest.raises(TypeError, match='The variable `test_data` must be a `SharedVariable`'):
        frozen_m.set_data('test_data', values=[2])
    with pytest.raises(TypeError, match='The dim_length of `test_dim` must be a `SharedVariable`'):
        frozen_m.set_dim('test_dim', new_length=6, coord_values=range(6))
with m:
    m.set_data('test_data', values=[2])
    m.set_dim('test_dim', new_length=6, coord_values=range(6))
assert m['test_data'].get_value() == [2]
assert m.dim_lengths['test_dim'].get_value() == 6
```

## Next Steps


---

*Source: test_optimization.py:29 | Complexity: Advanced | Last updated: 2026-05-18*