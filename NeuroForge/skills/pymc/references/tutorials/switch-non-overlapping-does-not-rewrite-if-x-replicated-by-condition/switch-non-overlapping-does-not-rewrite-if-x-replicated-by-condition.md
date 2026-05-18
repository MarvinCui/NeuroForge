# How To: Switch Non Overlapping Does Not Rewrite If X Replicated By Condition

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test switch non overlapping does not rewrite if x replicated by condition

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pymc`
- `pymc.logprob.basic`
- `pymc.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign scale = pt.scalar(...)

```python
scale = pt.scalar('scale')
```

### Step 2: Assign x = pm.Normal.dist(...)

```python
x = pm.Normal.dist(mu=0, sigma=1, size=(3,))
```

### Step 3: Assign cond = value

```python
cond = (x[None, :] > 0) & pt.ones((2, 1), dtype='bool')
```

### Step 4: Assign y = pt.switch(...)

```python
y = pt.switch(cond, x, scale * x)
```

### Step 5: Call logp()

```python
logp(y, np.zeros((2, 3)))
```


## Complete Example

```python
# Workflow
scale = pt.scalar('scale')
x = pm.Normal.dist(mu=0, sigma=1, size=(3,))
cond = (x[None, :] > 0) & pt.ones((2, 1), dtype='bool')
y = pt.switch(cond, x, scale * x)
with pytest.raises(NotImplementedError, match='Logprob method not implemented for Switch'):
    logp(y, np.zeros((2, 3)))
```

## Next Steps


---

*Source: test_switch.py:50 | Complexity: Intermediate | Last updated: 2026-05-18*