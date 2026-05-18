# How To: Do Prune

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test do prune

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: prune
```

## Step-by-Step Guide

### Step 1: Assign orig_named_vars = value

```python
orig_named_vars = {'x0', 'x1', 'y', 'y_det', 'z', 'llike'}
```

**Verification:**
```python
assert set(m.named_vars) == orig_named_vars
```

### Step 2: Assign do_m = do(...)

```python
do_m = do(m, {y_det: x0 + 5}, prune_vars=prune)
```

**Verification:**
```python
assert set(do_m.named_vars) == {'x0', 'x1', 'y_det', 'z', 'llike'}
```

### Step 3: Assign do_m = do(...)

```python
do_m = do(m, {z: 0.5}, prune_vars=prune)
```

**Verification:**
```python
assert set(do_m.named_vars) == orig_named_vars
```

### Step 4: Assign x0 = pm.Data(...)

```python
x0 = pm.Data('x0', 0)
```

**Verification:**
```python
assert set(do_m.named_vars) == {'x1', 'z', 'llike'}
```

### Step 5: Assign x1 = pm.Data(...)

```python
x1 = pm.Data('x1', 0)
```

**Verification:**
```python
assert set(do_m.named_vars) == orig_named_vars
```

### Step 6: Assign y = pm.Normal(...)

```python
y = pm.Normal('y')
```

### Step 7: Assign y_det = pm.Deterministic(...)

```python
y_det = pm.Deterministic('y_det', y + x0)
```

### Step 8: Assign z = pm.Normal(...)

```python
z = pm.Normal('z', y_det)
```

### Step 9: Assign llike = pm.Normal(...)

```python
llike = pm.Normal('llike', z + x1, observed=0)
```

**Verification:**
```python
assert set(do_m.named_vars) == {'x0', 'x1', 'y_det', 'z', 'llike'}
```


## Complete Example

```python
# Setup
# Fixtures: prune

# Workflow
with pm.Model() as m:
    x0 = pm.Data('x0', 0)
    x1 = pm.Data('x1', 0)
    y = pm.Normal('y')
    y_det = pm.Deterministic('y_det', y + x0)
    z = pm.Normal('z', y_det)
    llike = pm.Normal('llike', z + x1, observed=0)
orig_named_vars = {'x0', 'x1', 'y', 'y_det', 'z', 'llike'}
assert set(m.named_vars) == orig_named_vars
do_m = do(m, {y_det: x0 + 5}, prune_vars=prune)
if prune:
    assert set(do_m.named_vars) == {'x0', 'x1', 'y_det', 'z', 'llike'}
else:
    assert set(do_m.named_vars) == orig_named_vars
do_m = do(m, {z: 0.5}, prune_vars=prune)
if prune:
    assert set(do_m.named_vars) == {'x1', 'z', 'llike'}
else:
    assert set(do_m.named_vars) == orig_named_vars
```

## Next Steps


---

*Source: test_conditioning.py:242 | Complexity: Advanced | Last updated: 2026-05-18*