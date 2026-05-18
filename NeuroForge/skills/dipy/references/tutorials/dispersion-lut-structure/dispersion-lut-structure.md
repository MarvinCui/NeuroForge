# How To: Dispersion Lut Structure

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test dispersion_lut returns correct structure.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `dipy.sims.force`
- `dipy.sims.force`
- `dipy.core.gradients`
- `dipy.sims.force`
- `dipy.sims.force`
- `dipy.sims.force`


## Step-by-Step Guide

### Step 1: 'Test dispersion_lut returns correct structure.'

```python
'Test dispersion_lut returns correct structure.'
```

**Verification:**
```python
assert isinstance(result, dict)
```

### Step 2: Assign sphere = np.random.randn(...)

```python
sphere = np.random.randn(10, 3)
```

**Verification:**
```python
assert len(result) == 10
```

### Step 3: Assign sphere = value

```python
sphere = sphere / np.linalg.norm(sphere, axis=1, keepdims=True)
```

**Verification:**
```python
assert i in result
```

### Step 4: Assign odi_list = np.array(...)

```python
odi_list = np.array([0.1, 0.2, 0.3])
```

**Verification:**
```python
assert isinstance(result[i], dict)
```

### Step 5: Assign result = dispersion_lut(...)

```python
result = dispersion_lut(sphere, odi_list)
```

**Verification:**
```python
assert odi in result[i]
```


## Complete Example

```python
# Workflow
'Test dispersion_lut returns correct structure.'
sphere = np.random.randn(10, 3)
sphere = sphere / np.linalg.norm(sphere, axis=1, keepdims=True)
odi_list = np.array([0.1, 0.2, 0.3])
result = dispersion_lut(sphere, odi_list)
assert isinstance(result, dict)
assert len(result) == 10
for i in range(10):
    assert i in result
    assert isinstance(result[i], dict)
    for odi in odi_list:
        assert odi in result[i]
```

## Next Steps


---

*Source: test_force.py:14 | Complexity: Intermediate | Last updated: 2026-05-18*