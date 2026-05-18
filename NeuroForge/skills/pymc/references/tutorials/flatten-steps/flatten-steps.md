# How To: Flatten Steps

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test flatten steps

## Prerequisites

**Required Modules:**
- `pytensor`
- `pytest`
- `pymc`
- `pymc.step_methods`
- `pymc.step_methods.compound`
- `pymc.testing`
- `tests.helpers`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign a = pm.Normal(...)

```python
a = pm.Normal('a')
```

**Verification:**
```python
assert flatten_steps(s1) == [s1]
```

### Step 2: Assign b = pm.Normal(...)

```python
b = pm.Normal('b')
```

**Verification:**
```python
assert flatten_steps(c2) == [s1, s2, s3]
```

### Step 3: Assign c = pm.Normal(...)

```python
c = pm.Normal('c')
```

### Step 4: Assign s1 = Metropolis(...)

```python
s1 = Metropolis([a])
```

### Step 5: Assign s2 = Metropolis(...)

```python
s2 = Metropolis([b])
```

### Step 6: Assign c1 = CompoundStep(...)

```python
c1 = CompoundStep([s1, s2])
```

### Step 7: Assign s3 = NUTS(...)

```python
s3 = NUTS([c])
```

### Step 8: Assign c2 = CompoundStep(...)

```python
c2 = CompoundStep([c1, s3])
```

### Step 9: Call flatten_steps()

```python
flatten_steps('not a step')
```


## Complete Example

```python
# Workflow
with pm.Model():
    a = pm.Normal('a')
    b = pm.Normal('b')
    c = pm.Normal('c')
    s1 = Metropolis([a])
    s2 = Metropolis([b])
    c1 = CompoundStep([s1, s2])
    s3 = NUTS([c])
    c2 = CompoundStep([c1, s3])
assert flatten_steps(s1) == [s1]
assert flatten_steps(c2) == [s1, s2, s3]
with pytest.raises(ValueError, match='Unexpected type'):
    flatten_steps('not a step')
```

## Next Steps


---

*Source: test_compound.py:157 | Complexity: Advanced | Last updated: 2026-05-18*