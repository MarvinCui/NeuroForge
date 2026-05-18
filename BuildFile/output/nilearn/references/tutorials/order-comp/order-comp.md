# How To: Order Comp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test lt, gt, goe, loe.

## Prerequisites

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`


## Step-by-Step Guide

### Step 1: 'Test lt, gt, goe, loe.'

```python
'Test lt, gt, goe, loe.'
```

**Verification:**
```python
assert geq == '2016-08-12T11:29:12.263046Z'
```

### Step 2: Assign geq = neurovault.GreaterOrEqual(...)

```python
geq = neurovault.GreaterOrEqual('2016-07-12T11:29:12.263046Z')
```

**Verification:**
```python
assert geq != '2016-06-12T11:29:12.263046Z'
```

### Step 3: Assign gt = neurovault.GreaterThan(...)

```python
gt = neurovault.GreaterThan('abc')
```

**Verification:**
```python
assert str(geq) == "GreaterOrEqual('2016-07-12T11:29:12.263046Z')"
```

### Step 4: Assign lt = neurovault.LessThan(...)

```python
lt = neurovault.LessThan(7)
```

**Verification:**
```python
assert gt != 'abc'
```

### Step 5: Assign leq = neurovault.LessOrEqual(...)

```python
leq = neurovault.LessOrEqual(4.5)
```

**Verification:**
```python
assert gt == 'abd'
```


## Complete Example

```python
# Workflow
'Test lt, gt, goe, loe.'
geq = neurovault.GreaterOrEqual('2016-07-12T11:29:12.263046Z')
assert geq == '2016-08-12T11:29:12.263046Z'
assert geq != '2016-06-12T11:29:12.263046Z'
assert str(geq) == "GreaterOrEqual('2016-07-12T11:29:12.263046Z')"
gt = neurovault.GreaterThan('abc')
assert gt != 'abc'
assert gt == 'abd'
assert str(gt) == "GreaterThan('abc')"
lt = neurovault.LessThan(7)
assert lt != 7
assert lt == 5
assert lt != 'a'
assert str(lt) == 'LessThan(7)'
leq = neurovault.LessOrEqual(4.5)
assert leq == 4.4
assert leq != 4.6
assert str(leq) == 'LessOrEqual(4.5)'
```

## Next Steps


---

*Source: test_neurovault.py:370 | Complexity: Intermediate | Last updated: 2026-05-18*