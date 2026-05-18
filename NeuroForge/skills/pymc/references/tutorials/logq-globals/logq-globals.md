# How To: Logq Globals

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logq globals

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.testing`
- `pymc.variational`
- `pymc.variational.approximations`
- `tests.helpers`
- `cloudpickle`
- `cloudpickle`

**Setup Required:**
```python
# Fixtures: three_var_approx
```

## Step-by-Step Guide

### Step 1: Assign approx = three_var_approx

```python
approx = three_var_approx
```

**Verification:**
```python
assert e.shape == ()
```

### Step 2: Assign unknown = approx.set_size_and_deterministic(...)

```python
logq, symbolic_logq = approx.set_size_and_deterministic([approx.logq, approx.symbolic_logq], 1, 0)
```

**Verification:**
```python
assert es.shape == (1,)
```

### Step 3: Assign e = logq.eval(...)

```python
e = logq.eval()
```

**Verification:**
```python
assert e.shape == ()
```

### Step 4: Assign es = symbolic_logq.eval(...)

```python
es = symbolic_logq.eval()
```

**Verification:**
```python
assert es.shape == (2,)
```

### Step 5: Assign unknown = approx.set_size_and_deterministic(...)

```python
logq, symbolic_logq = approx.set_size_and_deterministic([approx.logq, approx.symbolic_logq], 2, 0)
```

### Step 6: Assign e = logq.eval(...)

```python
e = logq.eval()
```

### Step 7: Assign es = symbolic_logq.eval(...)

```python
es = symbolic_logq.eval()
```

**Verification:**
```python
assert e.shape == ()
```

### Step 8: Call pytest.skip()

```python
pytest.skip(f'{three_var_approx} does not implement logq')
```


## Complete Example

```python
# Setup
# Fixtures: three_var_approx

# Workflow
if not three_var_approx.has_logq:
    pytest.skip(f'{three_var_approx} does not implement logq')
approx = three_var_approx
logq, symbolic_logq = approx.set_size_and_deterministic([approx.logq, approx.symbolic_logq], 1, 0)
e = logq.eval()
es = symbolic_logq.eval()
assert e.shape == ()
assert es.shape == (1,)
logq, symbolic_logq = approx.set_size_and_deterministic([approx.logq, approx.symbolic_logq], 2, 0)
e = logq.eval()
es = symbolic_logq.eval()
assert e.shape == ()
assert es.shape == (2,)
```

## Next Steps


---

*Source: test_opvi.py:266 | Complexity: Advanced | Last updated: 2026-05-18*