# How To: Multiple Fast Inverse Errors

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multiple fast inverse errors

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.linalg`
- `scipy.stats`
- `numpy.testing`
- `scipy.stats`
- `nilearn._utils.data_gen`
- `nilearn.glm._utils`
- `nilearn.glm.first_level`
- `nilearn.maskers`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 2, 2)
```

### Step 2: Assign X = np.zeros(...)

```python
X = np.zeros(shape)
```

### Step 3: Assign shape = value

```python
shape = (10, 20, 20)
```

### Step 4: Assign X = np.zeros(...)

```python
X = np.zeros(shape)
```

### Step 5: Call multiple_fast_inverse()

```python
multiple_fast_inverse(X)
```

### Step 6: Call multiple_fast_inverse()

```python
multiple_fast_inverse(X)
```


## Complete Example

```python
# Workflow
shape = (2, 2, 2)
X = np.zeros(shape)
with pytest.raises(ValueError, match='Matrix LU decomposition failed'):
    multiple_fast_inverse(X)
shape = (10, 20, 20)
X = np.zeros(shape)
with pytest.raises(ValueError, match='Matrix LU decomposition failed'):
    multiple_fast_inverse(X)
```

## Next Steps


---

*Source: test_utils.py:217 | Complexity: Intermediate | Last updated: 2026-05-18*