# How To: Multidim Scaling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multidim scaling

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `pymc`
- `pymc`
- `pymc.data`
- `pymc.variational.minibatch_rv`


## Step-by-Step Guide

### Step 1: Assign _p0 = p0(...)

```python
_p0 = p0()
```

**Verification:**
```python
assert np.allclose(_p0, p1()) and np.allclose(_p0, p2()) and np.allclose(_p0, p3()) and np.allclose(_p0, p4()) and np.allclose(_p0, p5())
```

### Step 2: Call pm.Normal()

```python
pm.Normal('n', observed=[[1, 1], [1, 1]], total_size=[])
```

### Step 3: Assign p0 = pytensor.function(...)

```python
p0 = pytensor.function([], model0.logp())
```

### Step 4: Call pm.Normal()

```python
pm.Normal('n', observed=[[1, 1], [1, 1]], total_size=[2, 2])
```

### Step 5: Assign p1 = pytensor.function(...)

```python
p1 = pytensor.function([], model1.logp())
```

### Step 6: Call pm.Normal()

```python
pm.Normal('n', observed=[[1], [1]], total_size=[2, 2])
```

### Step 7: Assign p2 = pytensor.function(...)

```python
p2 = pytensor.function([], model2.logp())
```

### Step 8: Call pm.Normal()

```python
pm.Normal('n', observed=[[1, 1]], total_size=[2, 2])
```

### Step 9: Assign p3 = pytensor.function(...)

```python
p3 = pytensor.function([], model3.logp())
```

### Step 10: Call pm.Normal()

```python
pm.Normal('n', observed=[[1]], total_size=[2, 2])
```

### Step 11: Assign p4 = pytensor.function(...)

```python
p4 = pytensor.function([], model4.logp())
```

### Step 12: Call pm.Normal()

```python
pm.Normal('n', observed=[[1]], total_size=[2, Ellipsis, 2])
```

### Step 13: Assign p5 = pytensor.function(...)

```python
p5 = pytensor.function([], model5.logp())
```


## Complete Example

```python
# Workflow
with pm.Model() as model0:
    pm.Normal('n', observed=[[1, 1], [1, 1]], total_size=[])
    p0 = pytensor.function([], model0.logp())
with pm.Model() as model1:
    pm.Normal('n', observed=[[1, 1], [1, 1]], total_size=[2, 2])
    p1 = pytensor.function([], model1.logp())
with pm.Model() as model2:
    pm.Normal('n', observed=[[1], [1]], total_size=[2, 2])
    p2 = pytensor.function([], model2.logp())
with pm.Model() as model3:
    pm.Normal('n', observed=[[1, 1]], total_size=[2, 2])
    p3 = pytensor.function([], model3.logp())
with pm.Model() as model4:
    pm.Normal('n', observed=[[1]], total_size=[2, 2])
    p4 = pytensor.function([], model4.logp())
with pm.Model() as model5:
    pm.Normal('n', observed=[[1]], total_size=[2, Ellipsis, 2])
    p5 = pytensor.function([], model5.logp())
_p0 = p0()
assert np.allclose(_p0, p1()) and np.allclose(_p0, p2()) and np.allclose(_p0, p3()) and np.allclose(_p0, p4()) and np.allclose(_p0, p5())
```

## Next Steps


---

*Source: test_minibatch_rv.py:43 | Complexity: Advanced | Last updated: 2026-05-18*