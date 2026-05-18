# How To: Observe

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test observe

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

### Step 1: Assign m_new = observe(...)

```python
m_new = observe(m_old, {y: 0.5})
```

**Verification:**
```python
assert len(m_new.free_RVs) == 2
```

### Step 2: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(m_old.compile_logp()({'x': 0.9, 'y': 0.5, 'z': 1.4}), m_new.compile_logp()({'x': 0.9, 'z': 1.4}))
```

**Verification:**
```python
assert len(m_new.observed_RVs) == 1
```

### Step 3: Assign m_new = observe(...)

```python
m_new = observe(m_old, {y: 0.5, z: 1.4})
```

**Verification:**
```python
assert m_new['x'] in m_new.free_RVs
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(m_old.compile_logp()({'x': 0.9, 'y': 0.5, 'z': 1.4}), m_new.compile_logp()({'x': 0.9}))
```

**Verification:**
```python
assert m_new['y'] in m_new.observed_RVs
```

### Step 5: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

**Verification:**
```python
assert m_new['z'] in m_new.free_RVs
```

### Step 6: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x)
```

**Verification:**
```python
assert len(m_new.free_RVs) == 1
```

### Step 7: Assign z = pm.Normal(...)

```python
z = pm.Normal('z', y)
```

**Verification:**
```python
assert len(m_new.observed_RVs) == 2
```


## Complete Example

```python
# Workflow
with pm.Model() as m_old:
    x = pm.Normal('x')
    y = pm.Normal('y', x)
    z = pm.Normal('z', y)
m_new = observe(m_old, {y: 0.5})
assert len(m_new.free_RVs) == 2
assert len(m_new.observed_RVs) == 1
assert m_new['x'] in m_new.free_RVs
assert m_new['y'] in m_new.observed_RVs
assert m_new['z'] in m_new.free_RVs
np.testing.assert_allclose(m_old.compile_logp()({'x': 0.9, 'y': 0.5, 'z': 1.4}), m_new.compile_logp()({'x': 0.9, 'z': 1.4}))
m_new = observe(m_old, {y: 0.5, z: 1.4})
assert len(m_new.free_RVs) == 1
assert len(m_new.observed_RVs) == 2
assert m_new['x'] in m_new.free_RVs
assert m_new['y'] in m_new.observed_RVs
assert m_new['z'] in m_new.observed_RVs
np.testing.assert_allclose(m_old.compile_logp()({'x': 0.9, 'y': 0.5, 'z': 1.4}), m_new.compile_logp()({'x': 0.9}))
```

## Next Steps


---

*Source: test_conditioning.py:36 | Complexity: Intermediate | Last updated: 2026-05-18*