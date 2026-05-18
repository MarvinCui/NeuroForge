# How To: Remove Minibatches

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test remove minibatches

## Prerequisites

**Required Modules:**
- `numpy`
- `pymc`
- `pymc.model.transform.basic`


## Step-by-Step Guide

### Step 1: Assign data_size = 100

```python
data_size = 100
```

**Verification:**
```python
assert m1.y.shape[0].eval() == batch_size
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((data_size,))
```

**Verification:**
```python
assert m2.y.shape[0].eval() == data_size
```

### Step 3: Assign batch_size = 10

```python
batch_size = 10
```

**Verification:**
```python
assert m1.coords == m2.coords
```

### Step 4: Assign m2 = remove_minibatched_nodes(...)

```python
m2 = remove_minibatched_nodes(m1)
```

**Verification:**
```python
assert m1.dim_lengths['d'].eval() == m2.dim_lengths['d'].eval()
```

### Step 5: Assign mb = pm.Minibatch(...)

```python
mb = pm.Minibatch(data, batch_size=batch_size)
```

### Step 6: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', dims='d')
```

### Step 7: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 8: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x, observed=mb, total_size=100)
```


## Complete Example

```python
# Workflow
data_size = 100
data = np.zeros((data_size,))
batch_size = 10
with pm.Model(coords={'d': range(5)}) as m1:
    mb = pm.Minibatch(data, batch_size=batch_size)
    mu = pm.Normal('mu', dims='d')
    x = pm.Normal('x')
    y = pm.Normal('y', x, observed=mb, total_size=100)
m2 = remove_minibatched_nodes(m1)
assert m1.y.shape[0].eval() == batch_size
assert m2.y.shape[0].eval() == data_size
assert m1.coords == m2.coords
assert m1.dim_lengths['d'].eval() == m2.dim_lengths['d'].eval()
```

## Next Steps


---

*Source: test_basic.py:37 | Complexity: Advanced | Last updated: 2026-05-18*