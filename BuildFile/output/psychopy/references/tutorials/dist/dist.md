# How To: Dist

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the distance function in mathtools. This also test the `normalize`
function to ensure all vectors have a length of 1.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test the distance function in mathtools. This also test the `normalize`\n    function to ensure all vectors have a length of 1.\n\n    '

```python
'Test the distance function in mathtools. This also test the `normalize`\n    function to ensure all vectors have a length of 1.\n\n    '
```

**Verification:**
```python
assert np.allclose(distOneToMany, 1.0)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(123456)
```

**Verification:**
```python
assert np.allclose(distManyToOne, distOneToMany)
```

### Step 3: Assign N = 1000

```python
N = 1000
```

**Verification:**
```python
assert np.allclose(out, distManyToOne)
```

### Step 4: Assign vectors = normalize(...)

```python
vectors = normalize(np.random.uniform(-1.0, 1.0, (N, 3)))
```

**Verification:**
```python
assert id(out) == idToCheck
```

### Step 5: Assign distRowByRow = distance(...)

```python
distRowByRow = distance(np.zeros_like(vectors), vectors)
```

**Verification:**
```python
assert np.allclose(distRowByRow, 1.0)
```

### Step 6: Assign vectors = np.random.uniform(...)

```python
vectors = np.random.uniform(-1.0, 1.0, (N, nCol))
```

### Step 7: Assign vectors = normalize(...)

```python
vectors = normalize(vectors, out=vectors)
```

### Step 8: Assign point = np.zeros(...)

```python
point = np.zeros((nCol,))
```

### Step 9: Assign distOneToMany = distance(...)

```python
distOneToMany = distance(point, vectors)
```

**Verification:**
```python
assert np.allclose(distOneToMany, 1.0)
```

### Step 10: Assign distManyToOne = distance(...)

```python
distManyToOne = distance(point, vectors)
```

**Verification:**
```python
assert np.allclose(distManyToOne, distOneToMany)
```

### Step 11: Assign out = np.zeros(...)

```python
out = np.zeros((N,))
```

### Step 12: Assign idToCheck = id(...)

```python
idToCheck = id(out)
```

### Step 13: Assign out = distance(...)

```python
out = distance(vectors, point, out)
```

**Verification:**
```python
assert np.allclose(out, distManyToOne)
```


## Complete Example

```python
# Workflow
'Test the distance function in mathtools. This also test the `normalize`\n    function to ensure all vectors have a length of 1.\n\n    '
np.random.seed(123456)
N = 1000
for nCol in range(2, 4):
    vectors = np.random.uniform(-1.0, 1.0, (N, nCol))
    vectors = normalize(vectors, out=vectors)
    point = np.zeros((nCol,))
    distOneToMany = distance(point, vectors)
    assert np.allclose(distOneToMany, 1.0)
    distManyToOne = distance(point, vectors)
    assert np.allclose(distManyToOne, distOneToMany)
    out = np.zeros((N,))
    idToCheck = id(out)
    out = distance(vectors, point, out)
    assert np.allclose(out, distManyToOne)
    assert id(out) == idToCheck
vectors = normalize(np.random.uniform(-1.0, 1.0, (N, 3)))
distRowByRow = distance(np.zeros_like(vectors), vectors)
assert np.allclose(distRowByRow, 1.0)
```

## Next Steps


---

*Source: test_mathtools.py:258 | Complexity: Advanced | Last updated: 2026-05-18*