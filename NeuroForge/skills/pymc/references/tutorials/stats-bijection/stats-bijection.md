# How To: Stats Bijection

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test stats bijection

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

### Step 1: Assign step_stats_dtypes = value

```python
step_stats_dtypes = [{'a': float, 'b': int}, {'a': float, 'c': Warning}]
```

**Verification:**
```python
assert bij.object_stats == {'sampler_1__c': (1, 'c')}
```

### Step 2: Assign bij = StatsBijection(...)

```python
bij = StatsBijection(step_stats_dtypes)
```

**Verification:**
```python
assert bij.n_samplers == 2
```

### Step 3: Assign w = Warning(...)

```python
w = Warning('hmm')
```

**Verification:**
```python
assert isinstance(stats_d, dict)
```

### Step 4: Assign stats_l = value

```python
stats_l = [{'a': 1.5, 'b': 3}, {'a': 2.5, 'c': w}]
```

**Verification:**
```python
assert stats_d['sampler_0__a'] == 1.5
```

### Step 5: Assign stats_d = bij.map(...)

```python
stats_d = bij.map(stats_l)
```

**Verification:**
```python
assert stats_d['sampler_0__b'] == 3
```

### Step 6: Assign rev = bij.rmap(...)

```python
rev = bij.rmap(stats_d)
```

**Verification:**
```python
assert stats_d['sampler_1__a'] == 2.5
```

### Step 7: Assign rev2 = bij.rmap(...)

```python
rev2 = bij.rmap({'sampler_1__a': 0})
```

**Verification:**
```python
assert stats_d['sampler_1__c'] == w
```


## Complete Example

```python
# Workflow
step_stats_dtypes = [{'a': float, 'b': int}, {'a': float, 'c': Warning}]
bij = StatsBijection(step_stats_dtypes)
assert bij.object_stats == {'sampler_1__c': (1, 'c')}
assert bij.n_samplers == 2
w = Warning('hmm')
stats_l = [{'a': 1.5, 'b': 3}, {'a': 2.5, 'c': w}]
stats_d = bij.map(stats_l)
assert isinstance(stats_d, dict)
assert stats_d['sampler_0__a'] == 1.5
assert stats_d['sampler_0__b'] == 3
assert stats_d['sampler_1__a'] == 2.5
assert stats_d['sampler_1__c'] == w
rev = bij.rmap(stats_d)
assert isinstance(rev, list)
assert len(rev) == len(stats_l)
assert rev == stats_l
rev2 = bij.rmap({'sampler_1__a': 0})
assert len(rev2) == 2
assert len(rev2[0]) == 0
assert len(rev2[1]) == 1
```

## Next Steps


---

*Source: test_compound.py:172 | Complexity: Intermediate | Last updated: 2026-05-18*