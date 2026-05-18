# How To: Mode Is Kept

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mode is kept

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.raise_op`
- `pytensor.scan.utils`
- `scipy`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.scan`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: remove_asserts
```

## Step-by-Step Guide

### Step 1: Assign mode = value

```python
mode = Mode().including('local_remove_all_assert') if remove_asserts else None
```

**Verification:**
```python
assert x_logp(x=x_test_val)
```

### Step 2: Assign x = pytensor.scan(...)

```python
x = pytensor.scan(fn=lambda x: pt.random.normal(assert_op(x, x > 0)), outputs_info=[pt.ones(())], n_steps=10, mode=mode, return_updates=False)
```

### Step 3: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 4: Assign x_vv = x.clone(...)

```python
x_vv = x.clone()
```

### Step 5: Assign x_logp = pytensor.function(...)

```python
x_logp = pytensor.function([x_vv], pt.sum(logp(x, x_vv)))
```

### Step 6: Assign x_test_val = np.full(...)

```python
x_test_val = np.full((10,), -1)
```

**Verification:**
```python
assert x_logp(x=x_test_val)
```

### Step 7: Call x_logp()

```python
x_logp(x=x_test_val)
```


## Complete Example

```python
# Setup
# Fixtures: remove_asserts

# Workflow
mode = Mode().including('local_remove_all_assert') if remove_asserts else None
x = pytensor.scan(fn=lambda x: pt.random.normal(assert_op(x, x > 0)), outputs_info=[pt.ones(())], n_steps=10, mode=mode, return_updates=False)
x.name = 'x'
x_vv = x.clone()
x_logp = pytensor.function([x_vv], pt.sum(logp(x, x_vv)))
x_test_val = np.full((10,), -1)
if remove_asserts:
    assert x_logp(x=x_test_val)
else:
    with pytest.raises(AssertionError):
        x_logp(x=x_test_val)
```

## Next Steps


---

*Source: test_scan.py:392 | Complexity: Intermediate | Last updated: 2026-05-18*