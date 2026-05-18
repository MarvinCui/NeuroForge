# How To: Orderedlogistic Dimensions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test orderedlogistic dimensions

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `itertools`
- `sys`
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.tensor`
- `pymc`
- `pymc.distributions.discrete`
- `pymc.exceptions`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: shape
```

## Step-by-Step Guide

### Step 1: Assign loge = np.log10(...)

```python
loge = np.log10(np.exp(1))
```

**Verification:**
```python
assert c.owner.inputs[-1].type.shape == (1, *shape, 10)
```

### Step 2: Assign size = 7

```python
size = 7
```

**Verification:**
```python
assert np.allclose(clogp, expected)
```

### Step 3: Assign p = value

```python
p = np.ones((*shape, 10)) / 10
```

**Verification:**
```python
assert ol.owner.inputs[-1].type.shape == (1, *shape, 10)
```

### Step 4: Assign cutpoints = np.tile(...)

```python
cutpoints = np.tile(sp.logit(np.linspace(0, 1, 11)[1:-1]), (*shape, 1))
```

**Verification:**
```python
assert np.allclose(ologp, expected)
```

### Step 5: Assign obs = np.random.randint(...)

```python
obs = np.random.randint(0, 2, size=(size, *shape))
```

### Step 6: Assign ologp = value

```python
ologp = pm.logp(ol, np.ones_like(obs)).sum().eval() * loge
```

### Step 7: Assign clogp = value

```python
clogp = pm.logp(c, np.ones_like(obs)).sum().eval() * loge
```

### Step 8: Assign expected = value

```python
expected = -np.prod((size, *shape))
```

**Verification:**
```python
assert c.owner.inputs[-1].type.shape == (1, *shape, 10)
```

### Step 9: Assign ol = pm.OrderedLogistic(...)

```python
ol = pm.OrderedLogistic('ol', eta=np.zeros(shape), cutpoints=cutpoints, observed=obs)
```

### Step 10: Assign c = pm.Categorical(...)

```python
c = pm.Categorical('c', p=p, observed=obs)
```


## Complete Example

```python
# Setup
# Fixtures: shape

# Workflow
loge = np.log10(np.exp(1))
size = 7
p = np.ones((*shape, 10)) / 10
cutpoints = np.tile(sp.logit(np.linspace(0, 1, 11)[1:-1]), (*shape, 1))
obs = np.random.randint(0, 2, size=(size, *shape))
with pm.Model():
    ol = pm.OrderedLogistic('ol', eta=np.zeros(shape), cutpoints=cutpoints, observed=obs)
    c = pm.Categorical('c', p=p, observed=obs)
ologp = pm.logp(ol, np.ones_like(obs)).sum().eval() * loge
clogp = pm.logp(c, np.ones_like(obs)).sum().eval() * loge
expected = -np.prod((size, *shape))
assert c.owner.inputs[-1].type.shape == (1, *shape, 10)
assert np.allclose(clogp, expected)
assert ol.owner.inputs[-1].type.shape == (1, *shape, 10)
assert np.allclose(ologp, expected)
```

## Next Steps


---

*Source: test_discrete.py:500 | Complexity: Advanced | Last updated: 2026-05-18*