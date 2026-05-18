# How To: Dot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the dot-product function `dot()`. Tests cases Nx2, Nx3, and Nx4
including one-to-many cases. The test for the `cross()` function validates
if the values computed by `dot()` are meaningful.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test the dot-product function `dot()`. Tests cases Nx2, Nx3, and Nx4\n    including one-to-many cases. The test for the `cross()` function validates\n    if the values computed by `dot()` are meaningful.\n\n    '

```python
'Test the dot-product function `dot()`. Tests cases Nx2, Nx3, and Nx4\n    including one-to-many cases. The test for the `cross()` function validates\n    if the values computed by `dot()` are meaningful.\n\n    '
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(123456)
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 3: Assign N = 1000

```python
N = 1000
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 4: Assign vectors1 = np.random.uniform(...)

```python
vectors1 = np.random.uniform(-1.0, 1.0, (N, nCol))
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 5: Assign vectors2 = np.random.uniform(...)

```python
vectors2 = np.random.uniform(-1.0, 1.0, (N, nCol))
```

### Step 6: Assign results0 = dot(...)

```python
results0 = dot(vectors1, vectors2)
```

### Step 7: Assign results1 = np.zeros(...)

```python
results1 = np.zeros((N,))
```

### Step 8: Call dot()

```python
dot(vectors1, vectors2, out=results1)
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 9: Call results1.fill()

```python
results1.fill(0.0)
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 10: Assign results0 = dot(...)

```python
results0 = dot(vectors1[0, :], vectors2)
```

### Step 11: Call results1.fill()

```python
results1.fill(0.0)
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 12: Assign results0 = dot(...)

```python
results0 = dot(vectors1, vectors2[0, :])
```

### Step 13: Call results1.fill()

```python
results1.fill(0.0)
```

**Verification:**
```python
assert np.allclose(results0, results1)
```

### Step 14: Assign unknown = dot(...)

```python
results1[i] = dot(vectors1[i, :], vectors2[i, :])
```

### Step 15: Assign unknown = dot(...)

```python
results1[i] = dot(vectors1[0, :], vectors2[i, :])
```

### Step 16: Assign unknown = dot(...)

```python
results1[i] = dot(vectors1[i, :], vectors2[0, :])
```


## Complete Example

```python
# Workflow
'Test the dot-product function `dot()`. Tests cases Nx2, Nx3, and Nx4\n    including one-to-many cases. The test for the `cross()` function validates\n    if the values computed by `dot()` are meaningful.\n\n    '
np.random.seed(123456)
N = 1000
for nCol in range(2, 5):
    vectors1 = np.random.uniform(-1.0, 1.0, (N, nCol))
    vectors2 = np.random.uniform(-1.0, 1.0, (N, nCol))
    results0 = dot(vectors1, vectors2)
    results1 = np.zeros((N,))
    dot(vectors1, vectors2, out=results1)
    assert np.allclose(results0, results1)
    results1.fill(0.0)
    for i in range(N):
        results1[i] = dot(vectors1[i, :], vectors2[i, :])
    assert np.allclose(results0, results1)
    results0 = dot(vectors1[0, :], vectors2)
    results1.fill(0.0)
    for i in range(N):
        results1[i] = dot(vectors1[0, :], vectors2[i, :])
    assert np.allclose(results0, results1)
    results0 = dot(vectors1, vectors2[0, :])
    results1.fill(0.0)
    for i in range(N):
        results1[i] = dot(vectors1[i, :], vectors2[0, :])
    assert np.allclose(results0, results1)
```

## Next Steps


---

*Source: test_mathtools.py:211 | Complexity: Advanced | Last updated: 2026-05-18*