# How To: Basic Replace

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test basic replace

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `matplotlib.pyplot`
- `matplotlib.pyplot`


## Step-by-Step Guide

### Step 1: Assign unknown = pm.gp.util.replace_with_values(...)

```python
c_val, = pm.gp.util.replace_with_values([c], replacements={'a': 2, 'b': 3, 'x': 100}, model=model)
```

**Verification:**
```python
assert c_val == np.array(6.0)
```

### Step 2: Assign a = pm.Normal(...)

```python
a = pm.Normal('a')
```

### Step 3: Assign b = pm.Normal(...)

```python
b = pm.Normal('b', mu=a)
```

### Step 4: Assign c = value

```python
c = a * b
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    a = pm.Normal('a')
    b = pm.Normal('b', mu=a)
    c = a * b
c_val, = pm.gp.util.replace_with_values([c], replacements={'a': 2, 'b': 3, 'x': 100}, model=model)
assert c_val == np.array(6.0)
```

## Next Steps


---

*Source: test_util.py:74 | Complexity: Intermediate | Last updated: 2026-05-18*