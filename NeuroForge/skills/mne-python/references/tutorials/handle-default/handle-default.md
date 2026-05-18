# How To: Handle Default

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test mutable default.

## Prerequisites

**Required Modules:**
- `copy`
- `pytest`
- `numpy.testing`
- `mne.defaults`
- `mne.io.base`


## Step-by-Step Guide

### Step 1: 'Test mutable default.'

```python
'Test mutable default.'
```

**Verification:**
```python
assert set(x.keys()) == set(y.keys())
```

### Step 2: Assign x = deepcopy(...)

```python
x = deepcopy(_handle_default('scalings'))
```

**Verification:**
```python
assert set(x.keys()) == set(z.keys())
```

### Step 3: Assign y = _handle_default(...)

```python
y = _handle_default('scalings')
```

**Verification:**
```python
assert x[key] == y[key]
```

### Step 4: Assign z = _handle_default(...)

```python
z = _handle_default('scalings', dict(mag=1, grad=2))
```

**Verification:**
```python
assert x[key] == w[key]
```

### Step 5: Assign w = _handle_default(...)

```python
w = _handle_default('scalings', {})
```

**Verification:**
```python
assert x[key] != z[key]
```


## Complete Example

```python
# Workflow
'Test mutable default.'
x = deepcopy(_handle_default('scalings'))
y = _handle_default('scalings')
z = _handle_default('scalings', dict(mag=1, grad=2))
w = _handle_default('scalings', {})
assert set(x.keys()) == set(y.keys())
assert set(x.keys()) == set(z.keys())
for key in x.keys():
    assert x[key] == y[key]
    assert x[key] == w[key]
    if key in ('mag', 'grad'):
        assert x[key] != z[key]
    else:
        assert x[key] == z[key]
```

## Next Steps


---

*Source: test_defaults.py:14 | Complexity: Intermediate | Last updated: 2026-05-18*