# How To: Euler Instability

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test euler instability

## Prerequisites

**Required Modules:**
- `math`
- `numpy`
- `numpy`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign po2 = value

```python
po2 = pi / 2
```

### Step 2: Assign zyx = value

```python
zyx = (po2, po2, po2)
```

### Step 3: Assign M = nea.euler2mat(...)

```python
M = nea.euler2mat(*zyx)
```

### Step 4: Assign M_back = nea.euler2mat(...)

```python
M_back = nea.euler2mat(*nea.mat2euler(M))
```

### Step 5: yield (assert_true, np.allclose(M, M_back))

```python
yield (assert_true, np.allclose(M, M_back))
```

### Step 6: Assign M_e = value

```python
M_e = M - FLOAT_EPS
```

### Step 7: Assign M_e_back = nea.euler2mat(...)

```python
M_e_back = nea.euler2mat(*nea.mat2euler(M_e))
```

### Step 8: yield (assert_true, np.allclose(M_e, M_e_back))

```python
yield (assert_true, np.allclose(M_e, M_e_back))
```

### Step 9: Assign M_e_back = nea.euler2mat(...)

```python
M_e_back = nea.euler2mat(*crude_mat2euler(M_e))
```

### Step 10: yield (assert_false, np.allclose(M_e, M_e_back))

```python
yield (assert_false, np.allclose(M_e, M_e_back))
```


## Complete Example

```python
# Workflow
po2 = pi / 2
zyx = (po2, po2, po2)
M = nea.euler2mat(*zyx)
M_back = nea.euler2mat(*nea.mat2euler(M))
yield (assert_true, np.allclose(M, M_back))
M_e = M - FLOAT_EPS
M_e_back = nea.euler2mat(*nea.mat2euler(M_e))
yield (assert_true, np.allclose(M_e, M_e_back))
M_e_back = nea.euler2mat(*crude_mat2euler(M_e))
yield (assert_false, np.allclose(M_e, M_e_back))
```

## Next Steps


---

*Source: test_euler.py:140 | Complexity: Advanced | Last updated: 2026-05-18*