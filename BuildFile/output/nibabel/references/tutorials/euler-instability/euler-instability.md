# How To: Euler Instability

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test euler instability

## Prerequisites

**Required Modules:**
- `math`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign po2 = value

```python
po2 = pi / 2
```

**Verification:**
```python
assert np.allclose(M, M_back)
```

### Step 2: Assign zyx = value

```python
zyx = (po2, po2, po2)
```

**Verification:**
```python
assert np.allclose(M_e, M_e_back)
```

### Step 3: Assign M = nea.euler2mat(...)

```python
M = nea.euler2mat(*zyx)
```

**Verification:**
```python
assert not np.allclose(M_e, M_e_back)
```

### Step 4: Assign M_back = nea.euler2mat(...)

```python
M_back = nea.euler2mat(*nea.mat2euler(M))
```

**Verification:**
```python
assert np.allclose(M, M_back)
```

### Step 5: Assign M_e = value

```python
M_e = M - FLOAT_EPS
```

### Step 6: Assign M_e_back = nea.euler2mat(...)

```python
M_e_back = nea.euler2mat(*nea.mat2euler(M_e))
```

**Verification:**
```python
assert np.allclose(M_e, M_e_back)
```

### Step 7: Assign M_e_back = nea.euler2mat(...)

```python
M_e_back = nea.euler2mat(*crude_mat2euler(M_e))
```

**Verification:**
```python
assert not np.allclose(M_e, M_e_back)
```


## Complete Example

```python
# Workflow
po2 = pi / 2
zyx = (po2, po2, po2)
M = nea.euler2mat(*zyx)
M_back = nea.euler2mat(*nea.mat2euler(M))
assert np.allclose(M, M_back)
M_e = M - FLOAT_EPS
M_e_back = nea.euler2mat(*nea.mat2euler(M_e))
assert np.allclose(M_e, M_e_back)
M_e_back = nea.euler2mat(*crude_mat2euler(M_e))
assert not np.allclose(M_e, M_e_back)
```

## Next Steps


---

*Source: test_euler.py:156 | Complexity: Intermediate | Last updated: 2026-05-18*