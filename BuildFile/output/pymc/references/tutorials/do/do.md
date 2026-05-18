# How To: Do

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test do

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

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(seed=435)
```

**Verification:**
```python
assert -5 < pm.draw(z, random_seed=rng) < 5
```

### Step 2: Assign m_new = do(...)

```python
m_new = do(m_old, {y: x + 100})
```

**Verification:**
```python
assert len(m_new.free_RVs) == 2
```

### Step 3: Assign m_new = do(...)

```python
m_new = do(m_old, {y: 100 * switch, x: 100 * switch})
```

**Verification:**
```python
assert m_new['x'] in m_new.free_RVs
```

### Step 4: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, 0.001)
```

**Verification:**
```python
assert m_new['y'] in m_new.deterministics
```

### Step 5: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x, 0.001)
```

**Verification:**
```python
assert m_new['z'] in m_new.free_RVs
```

### Step 6: Assign z = pm.Normal(...)

```python
z = pm.Normal('z', y + x, 0.001)
```

**Verification:**
```python
assert 95 < pm.draw(m_new['z'], random_seed=rng) < 105
```

### Step 7: Assign switch = pm.Data(...)

```python
switch = pm.Data('switch', 1)
```

**Verification:**
```python
assert len(m_new.free_RVs) == 1
```

### Step 8: Call pm.set_data()

```python
pm.set_data({'switch': 0})
```

**Verification:**
```python
assert m_new['y'] not in m_new.deterministics
```


## Complete Example

```python
# Workflow
rng = np.random.default_rng(seed=435)
with pm.Model() as m_old:
    x = pm.Normal('x', 0, 0.001)
    y = pm.Normal('y', x, 0.001)
    z = pm.Normal('z', y + x, 0.001)
assert -5 < pm.draw(z, random_seed=rng) < 5
m_new = do(m_old, {y: x + 100})
assert len(m_new.free_RVs) == 2
assert m_new['x'] in m_new.free_RVs
assert m_new['y'] in m_new.deterministics
assert m_new['z'] in m_new.free_RVs
assert 95 < pm.draw(m_new['z'], random_seed=rng) < 105
with m_old:
    switch = pm.Data('switch', 1)
m_new = do(m_old, {y: 100 * switch, x: 100 * switch})
assert len(m_new.free_RVs) == 1
assert m_new['y'] not in m_new.deterministics
assert m_new['x'] not in m_new.deterministics
assert m_new['z'] in m_new.free_RVs
assert 195 < pm.draw(m_new['z'], random_seed=rng) < 205
with m_new:
    pm.set_data({'switch': 0})
assert -5 < pm.draw(m_new['z'], random_seed=rng) < 5
```

## Next Steps


---

*Source: test_conditioning.py:138 | Complexity: Advanced | Last updated: 2026-05-18*