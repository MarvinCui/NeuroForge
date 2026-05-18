# How To: Length

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test function `length()`.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test function `length()`.'

```python
'Test function `length()`.'
```

**Verification:**
```python
assert np.allclose(result0, result1)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(123456)
```

**Verification:**
```python
assert np.allclose(result0, np.sqrt(result1))
```

### Step 3: Assign N = 1000

```python
N = 1000
```

**Verification:**
```python
assert np.allclose(result0, result1)
```

### Step 4: Assign v = np.random.uniform(...)

```python
v = np.random.uniform(-1.0, 1.0, (N, 3))
```

### Step 5: Assign result0 = length(...)

```python
result0 = length(v)
```

### Step 6: Assign result1 = np.zeros(...)

```python
result1 = np.zeros((N,))
```

### Step 7: Call length()

```python
length(v, out=result1)
```

**Verification:**
```python
assert np.allclose(result0, result1)
```

### Step 8: Assign result1 = length(...)

```python
result1 = length(v, squared=True)
```

**Verification:**
```python
assert np.allclose(result0, np.sqrt(result1))
```

### Step 9: Assign result1 = np.zeros(...)

```python
result1 = np.zeros((N,))
```

**Verification:**
```python
assert np.allclose(result0, result1)
```

### Step 10: Assign unknown = length(...)

```python
result1[i] = length(v[i, :])
```


## Complete Example

```python
# Workflow
'Test function `length()`.'
np.random.seed(123456)
N = 1000
v = np.random.uniform(-1.0, 1.0, (N, 3))
result0 = length(v)
result1 = np.zeros((N,))
length(v, out=result1)
assert np.allclose(result0, result1)
result1 = length(v, squared=True)
assert np.allclose(result0, np.sqrt(result1))
result1 = np.zeros((N,))
for i in range(N):
    result1[i] = length(v[i, :])
assert np.allclose(result0, result1)
```

## Next Steps


---

*Source: test_mathtools.py:183 | Complexity: Advanced | Last updated: 2026-05-18*