# How To: Intermediate Rv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that function replaces values above an intermediate RV.

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

### Step 1: 'Test that function replaces values above an intermediate RV.'

```python
'Test that function replaces values above an intermediate RV.'
```

**Verification:**
```python
assert len([n for n in res_ancestors if n.owner and isinstance(n.owner.op, MeasurableOp)]) == 1
```

### Step 2: Assign a = pt.random.uniform(...)

```python
a = pt.random.uniform(0.0, 1.0)
```

**Verification:**
```python
assert c_value_var in res_ancestors
```

### Step 3: Assign a.name = 'a'

```python
a.name = 'a'
```

**Verification:**
```python
assert a_value_var in res_ancestors
```

### Step 4: Assign a.tag.value_var, a_value_var = a.clone(...)

```python
a.tag.value_var = a_value_var = a.clone()
```

### Step 5: Assign b = pt.random.uniform(...)

```python
b = pt.random.uniform(0, a + 1.0)
```

### Step 6: Assign b.name = 'b'

```python
b.name = 'b'
```

### Step 7: Assign b.tag.value_var = b.clone(...)

```python
b.tag.value_var = b.clone()
```

### Step 8: Assign c = pt.random.normal(...)

```python
c = pt.random.normal()
```

### Step 9: Assign c.name = 'c'

```python
c.name = 'c'
```

### Step 10: Assign c.tag.value_var, c_value_var = c.clone(...)

```python
c.tag.value_var = c_value_var = c.clone()
```

### Step 11: Assign d = value

```python
d = pt.log(c + b) + 2.0
```

### Step 12: Assign initial_replacements = value

```python
initial_replacements = {a: a_value_var, c: c_value_var}
```

### Step 13: Assign unknown = replace_rvs_by_values(...)

```python
res, = replace_rvs_by_values((d,), rvs_to_values=initial_replacements)
```

### Step 14: Assign res_ancestors = list(...)

```python
res_ancestors = list(ancestors((res,)))
```

**Verification:**
```python
assert len([n for n in res_ancestors if n.owner and isinstance(n.owner.op, MeasurableOp)]) == 1
```


## Complete Example

```python
# Workflow
'Test that function replaces values above an intermediate RV.'
a = pt.random.uniform(0.0, 1.0)
a.name = 'a'
a.tag.value_var = a_value_var = a.clone()
b = pt.random.uniform(0, a + 1.0)
b.name = 'b'
b.tag.value_var = b.clone()
c = pt.random.normal()
c.name = 'c'
c.tag.value_var = c_value_var = c.clone()
d = pt.log(c + b) + 2.0
initial_replacements = {a: a_value_var, c: c_value_var}
res, = replace_rvs_by_values((d,), rvs_to_values=initial_replacements)
res_ancestors = list(ancestors((res,)))
assert len([n for n in res_ancestors if n.owner and isinstance(n.owner.op, MeasurableOp)]) == 1
assert c_value_var in res_ancestors
assert a_value_var in res_ancestors
```

## Next Steps


---

*Source: test_utils.py:133 | Complexity: Advanced | Last updated: 2026-05-18*