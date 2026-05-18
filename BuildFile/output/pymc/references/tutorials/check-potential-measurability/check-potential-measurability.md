# How To: Check Potential Measurability

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check potential measurability

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.graph.replace`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign x1 = pt.random.normal(...)

```python
x1 = pt.random.normal()
```

**Verification:**
```python
assert check_potential_measurability([y])
```

### Step 2: Assign x1_valued = valued_rv(...)

```python
x1_valued = valued_rv(x1, x1.type())
```

**Verification:**
```python
assert check_potential_measurability([y])
```

### Step 3: Assign x2 = pt.random.normal(...)

```python
x2 = pt.random.normal()
```

**Verification:**
```python
assert check_potential_measurability([y])
```

### Step 4: Assign x2_valued = valued_rv(...)

```python
x2_valued = valued_rv(x2, x2.type())
```

**Verification:**
```python
assert not check_potential_measurability([y])
```

### Step 5: Assign x3 = pt.scalar(...)

```python
x3 = pt.scalar('x3')
```

### Step 6: Assign y = pt.exp(...)

```python
y = pt.exp(x1 + x2 + x3)
```

**Verification:**
```python
assert check_potential_measurability([y])
```

### Step 7: Assign y = pt.exp(...)

```python
y = pt.exp(x1_valued + x2 + x3)
```

**Verification:**
```python
assert check_potential_measurability([y])
```

### Step 8: Assign y = pt.exp(...)

```python
y = pt.exp(x1 + x2_valued + x3)
```

**Verification:**
```python
assert check_potential_measurability([y])
```

### Step 9: Assign y = pt.exp(...)

```python
y = pt.exp(x1_valued + x2_valued + x3)
```

**Verification:**
```python
assert not check_potential_measurability([y])
```


## Complete Example

```python
# Workflow
x1 = pt.random.normal()
x1_valued = valued_rv(x1, x1.type())
x2 = pt.random.normal()
x2_valued = valued_rv(x2, x2.type())
x3 = pt.scalar('x3')
y = pt.exp(x1 + x2 + x3)
assert check_potential_measurability([y])
y = pt.exp(x1_valued + x2 + x3)
assert check_potential_measurability([y])
y = pt.exp(x1 + x2_valued + x3)
assert check_potential_measurability([y])
y = pt.exp(x1_valued + x2_valued + x3)
assert not check_potential_measurability([y])
```

## Next Steps


---

*Source: test_utils.py:311 | Complexity: Advanced | Last updated: 2026-05-18*