# How To: Warn Treedepth Multiple Samplers

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check we handle cases when sampling with multiple NUTS samplers, each of which reports max_treedepth.

## Prerequisites

**Required Modules:**
- `logging`
- `arviz`
- `numpy`
- `pytest`
- `pymc.stats`


## Step-by-Step Guide

### Step 1: 'Check we handle cases when sampling with multiple NUTS samplers, each of which reports max_treedepth.'

```python
'Check we handle cases when sampling with multiple NUTS samplers, each of which reports max_treedepth.'
```

**Verification:**
```python
assert len(warns) == 2
```

### Step 2: Assign max_treedepth = np.zeros(...)

```python
max_treedepth = np.zeros((3, 2, 2), dtype=bool)
```

**Verification:**
```python
assert 'Chain 0 reached the maximum tree depth' in warns[0].message
```

### Step 3: Assign unknown = True

```python
max_treedepth[0, 0, 0] = True
```

**Verification:**
```python
assert 'Chain 2 reached the maximum tree depth' in warns[1].message
```

### Step 4: Assign unknown = True

```python
max_treedepth[2, 1, 1] = True
```

### Step 5: Assign idata = arviz.from_dict(...)

```python
idata = arviz.from_dict({'sample_stats': {'reached_max_treedepth': max_treedepth}})
```

### Step 6: Assign warns = convergence.warn_treedepth(...)

```python
warns = convergence.warn_treedepth(idata)
```

**Verification:**
```python
assert len(warns) == 2
```


## Complete Example

```python
# Workflow
'Check we handle cases when sampling with multiple NUTS samplers, each of which reports max_treedepth.'
max_treedepth = np.zeros((3, 2, 2), dtype=bool)
max_treedepth[0, 0, 0] = True
max_treedepth[2, 1, 1] = True
idata = arviz.from_dict({'sample_stats': {'reached_max_treedepth': max_treedepth}})
warns = convergence.warn_treedepth(idata)
assert len(warns) == 2
assert 'Chain 0 reached the maximum tree depth' in warns[0].message
assert 'Chain 2 reached the maximum tree depth' in warns[1].message
```

## Next Steps


---

*Source: test_convergence.py:57 | Complexity: Intermediate | Last updated: 2026-05-18*