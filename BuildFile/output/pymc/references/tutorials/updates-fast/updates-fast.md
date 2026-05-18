# How To: Updates Fast

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test updates fast

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pymc.variational.updates`

**Setup Required:**
```python
# Fixtures: opt, loss_and_params, kwargs, getter
```

## Step-by-Step Guide

### Step 1: Assign unknown = getter(...)

```python
loss, param = getter(loss_and_params)
```

**Verification:**
```python
assert callable(updates)
```

### Step 2: Assign args = value

```python
args = {}
```

**Verification:**
```python
assert isinstance(updates, dict)
```

### Step 3: Call args.update()

```python
args.update(**kwargs)
```

**Verification:**
```python
assert isinstance(updates, dict)
```

### Step 4: Call args.update()

```python
args.update({'loss_or_grads': loss, 'params': param})
```

### Step 5: Assign updates = opt(...)

```python
updates = opt(**args)
```

**Verification:**
```python
assert callable(updates)
```

### Step 6: Assign updates = opt(...)

```python
updates = opt(_b, [_a])
```

**Verification:**
```python
assert isinstance(updates, dict)
```

### Step 7: Assign updates = opt(...)

```python
updates = opt(**args)
```

**Verification:**
```python
assert isinstance(updates, dict)
```

### Step 8: Call opt()

```python
opt(**args)
```


## Complete Example

```python
# Setup
# Fixtures: opt, loss_and_params, kwargs, getter

# Workflow
loss, param = getter(loss_and_params)
args = {}
args.update(**kwargs)
args.update({'loss_or_grads': loss, 'params': param})
if loss is None and param is None:
    updates = opt(**args)
    assert callable(updates)
    updates = opt(_b, [_a])
    assert isinstance(updates, dict)
elif loss is None or param is None:
    with pytest.raises(ValueError):
        opt(**args)
else:
    updates = opt(**args)
    assert isinstance(updates, dict)
```

## Next Steps


---

*Source: test_updates.py:71 | Complexity: Advanced | Last updated: 2026-05-18*