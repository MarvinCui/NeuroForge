# How To: Is Spd With Non Symmetrical Matrix

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test is spd with non symmetrical matrix

## Prerequisites

**Required Modules:**
- `numpy`
- `nilearn._utils.extmath`


## Step-by-Step Guide

### Step 1: Assign matrix = np.arange.reshape(...)

```python
matrix = np.arange(4).reshape(4, 1)
```

**Verification:**
```python
assert not is_spd(matrix)
```

### Step 2: Assign matrix = np.array(...)

```python
matrix = np.array([[1, 0.001 + 9e-19], [0.001, 1]])
```

**Verification:**
```python
assert is_spd(matrix)
```

### Step 3: Assign matrix = np.array(...)

```python
matrix = np.array([[1, 0.001 + 1e-18], [0.001, 1]])
```

**Verification:**
```python
assert not is_spd(matrix)
```

### Step 4: Assign matrix = np.array(...)

```python
matrix = np.array([[1, 0.001 + 9e-08], [0.001, 1]])
```

**Verification:**
```python
assert is_spd(matrix, decimal=4)
```

### Step 5: Assign matrix = np.array(...)

```python
matrix = np.array([[1, 0.001 + 1e-07], [0.001, 1]])
```

**Verification:**
```python
assert not is_spd(matrix, decimal=4)
```


## Complete Example

```python
# Workflow
matrix = np.arange(4).reshape(4, 1)
assert not is_spd(matrix)
matrix = np.array([[1, 0.001 + 9e-19], [0.001, 1]])
assert is_spd(matrix)
matrix = np.array([[1, 0.001 + 1e-18], [0.001, 1]])
assert not is_spd(matrix)
matrix = np.array([[1, 0.001 + 9e-08], [0.001, 1]])
assert is_spd(matrix, decimal=4)
matrix = np.array([[1, 0.001 + 1e-07], [0.001, 1]])
assert not is_spd(matrix, decimal=4)
```

## Next Steps


---

*Source: test_extmath.py:15 | Complexity: Intermediate | Last updated: 2026-05-18*