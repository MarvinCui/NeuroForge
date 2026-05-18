# How To: Observe Minibatch

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test observe minibatch

## Prerequisites

**Required Modules:**
- `arviz`
- `numpy`
- `pytest`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.variational.minibatch_rv`


## Step-by-Step Guide

### Step 1: Assign data = np.zeros(...)

```python
data = np.zeros((100,), dtype=config.floatX)
```

**Verification:**
```python
assert len(m_new.free_RVs) == 2
```

### Step 2: Assign batch_size = 10

```python
batch_size = 10
```

**Verification:**
```python
assert len(m_new.observed_RVs) == 1
```

### Step 3: Assign mb_data = pm.Minibatch(...)

```python
mb_data = pm.Minibatch(data, batch_size=batch_size)
```

**Verification:**
```python
assert m_new['x'] in m_new.free_RVs
```

### Step 4: Assign m_new = observe(...)

```python
m_new = observe(m_old, {mb_z: mb_data})
```

**Verification:**
```python
assert m_new['y'] in m_new.free_RVs
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(m_old.compile_logp()({'x': 0.9, 'y': 0.5, 'mb_z': np.zeros(10)}), m_new.compile_logp()({'x': 0.9, 'y': 0.5}))
```

**Verification:**
```python
assert m_new['mb_z'] in m_new.observed_RVs
```

### Step 6: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 7: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x)
```

### Step 8: Assign z_raw = pm.Normal.dist(...)

```python
z_raw = pm.Normal.dist(y, shape=batch_size)
```

### Step 9: Assign mb_z = create_minibatch_rv(...)

```python
mb_z = create_minibatch_rv(z_raw, total_size=data.shape)
```

### Step 10: Call m_old.register_rv()

```python
m_old.register_rv(mb_z, name='mb_z')
```


## Complete Example

```python
# Workflow
data = np.zeros((100,), dtype=config.floatX)
batch_size = 10
with pm.Model() as m_old:
    x = pm.Normal('x')
    y = pm.Normal('y', x)
    z_raw = pm.Normal.dist(y, shape=batch_size)
    mb_z = create_minibatch_rv(z_raw, total_size=data.shape)
    m_old.register_rv(mb_z, name='mb_z')
mb_data = pm.Minibatch(data, batch_size=batch_size)
m_new = observe(m_old, {mb_z: mb_data})
assert len(m_new.free_RVs) == 2
assert len(m_new.observed_RVs) == 1
assert m_new['x'] in m_new.free_RVs
assert m_new['y'] in m_new.free_RVs
assert m_new['mb_z'] in m_new.observed_RVs
np.testing.assert_allclose(m_old.compile_logp()({'x': 0.9, 'y': 0.5, 'mb_z': np.zeros(10)}), m_new.compile_logp()({'x': 0.9, 'y': 0.5}))
```

## Next Steps


---

*Source: test_conditioning.py:70 | Complexity: Advanced | Last updated: 2026-05-18*