# How To: Model Graph With Intermediate Named Variables

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test model graph with intermediate named variables

## Prerequisites

**Required Modules:**
- `warnings`
- `textwrap`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.compile.sharedvalue`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.exceptions`
- `pymc.model_graph`


## Step-by-Step Guide

### Step 1: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', 0, 1, shape=3)
```

**Verification:**
```python
assert ModelGraph(m1).make_compute_graph() == {'a': set(), 'b': {'a'}}
```

### Step 2: Call pm.Normal()

```python
pm.Normal('b', a.mean(axis=-1), 1)
```

**Verification:**
```python
assert ModelGraph(m2).make_compute_graph() == {'a': set(), 'c': {'a'}}
```

### Step 3: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', 0, 1)
```

**Verification:**
```python
assert ModelGraph(m3).make_compute_graph() == {'C': set(), 'D': set(), 'E': {'C'}}
```

### Step 4: Assign b = value

```python
b = a + 1
```

### Step 5: Assign b.name = 'b'

```python
b.name = 'b'
```

### Step 6: Call pm.Normal()

```python
pm.Normal('c', b, 1)
```

### Step 7: Assign data = pt.as_tensor_variable(...)

```python
data = pt.as_tensor_variable(np.ones((5, 3)), name='C')
```

### Step 8: Assign C = pm.Deterministic(...)

```python
C = pm.Deterministic('C', data)
```

### Step 9: Assign D = pm.Deterministic(...)

```python
D = pm.Deterministic('D', data)
```

### Step 10: Assign E = pm.Deterministic(...)

```python
E = pm.Deterministic('E', C)
```


## Complete Example

```python
# Workflow
with pm.Model() as m1:
    a = pm.Normal('a', 0, 1, shape=3)
    pm.Normal('b', a.mean(axis=-1), 1)
assert ModelGraph(m1).make_compute_graph() == {'a': set(), 'b': {'a'}}
with pm.Model() as m2:
    a = pm.Normal('a', 0, 1)
    b = a + 1
    b.name = 'b'
    pm.Normal('c', b, 1)
assert ModelGraph(m2).make_compute_graph() == {'a': set(), 'c': {'a'}}
with pm.Model() as m3:
    data = pt.as_tensor_variable(np.ones((5, 3)), name='C')
    C = pm.Deterministic('C', data)
    D = pm.Deterministic('D', data)
    E = pm.Deterministic('E', C)
assert ModelGraph(m3).make_compute_graph() == {'C': set(), 'D': set(), 'E': {'C'}}
```

## Next Steps


---

*Source: test_model_graph.py:514 | Complexity: Advanced | Last updated: 2026-05-18*