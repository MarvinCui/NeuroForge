# How To: Get Params

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test get params

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `traceback`
- `pytest`
- `nilearn.decoding.space_net`

**Setup Required:**
```python
# Fixtures: penalty, param, estimator
```

## Step-by-Step Guide

### Step 1: Assign kwargs = value

```python
kwargs = {}
```

**Verification:**
```python
assert param in params, f"{m} doesn't have parameter '{param}'."
```

### Step 2: Assign m = estimator(...)

```python
m = estimator(mask='dummy', penalty=penalty, **kwargs)
```

**Verification:**
```python
assert param in params, f"{m} doesn't have parameter '{param}'."
```

### Step 3: Assign params = m.get_params(...)

```python
params = m.get_params()
```

### Step 4: Assign params = m._get_params(...)

```python
params = m._get_params()
```


## Complete Example

```python
# Setup
# Fixtures: penalty, param, estimator

# Workflow
kwargs = {}
m = estimator(mask='dummy', penalty=penalty, **kwargs)
try:
    params = m.get_params()
except AttributeError:
    if 'get_params' in traceback.format_exc():
        params = m._get_params()
    else:
        raise
assert param in params, f"{m} doesn't have parameter '{param}'."
```

## Next Steps


---

*Source: test_sklearn_compatibility.py:24 | Complexity: Advanced | Last updated: 2026-05-18*