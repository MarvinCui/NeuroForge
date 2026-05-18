# How To: Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if `transform` gives the same results as a matrix.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test if `transform` gives the same results as a matrix.'

```python
'Test if `transform` gives the same results as a matrix.'
```

**Verification:**
```python
assert np.allclose(tPoint, mPoint[:, :3])
```

### Step 2: Call np.random.seed()

```python
np.random.seed(123456)
```

### Step 3: Assign N = 1000

```python
N = 1000
```

### Step 4: Assign axes = np.random.uniform(...)

```python
axes = np.random.uniform(-1.0, 1.0, (N, 3))
```

### Step 5: Assign angles = np.random.uniform(...)

```python
angles = np.random.uniform(0.0, 360.0, (N,))
```

### Step 6: Assign translations = np.random.uniform(...)

```python
translations = np.random.uniform(-10.0, 10.0, (N, 3))
```

### Step 7: Assign points = np.zeros(...)

```python
points = np.zeros((N, 4))
```

### Step 8: Assign unknown = np.random.uniform(...)

```python
points[:, :3] = np.random.uniform(-10.0, 10.0, (N, 3))
```

### Step 9: Assign unknown = 1.0

```python
points[:, 3] = 1.0
```

### Step 10: Assign ori = quatFromAxisAngle(...)

```python
ori = quatFromAxisAngle(axes[i, :], angles[i], degrees=True)
```

### Step 11: Assign rm = rotationMatrix(...)

```python
rm = rotationMatrix(angles[i], axes[i, :])
```

### Step 12: Assign tm = translationMatrix(...)

```python
tm = translationMatrix(translations[i, :])
```

### Step 13: Assign m = concatenate(...)

```python
m = concatenate([rm, tm])
```

### Step 14: Assign tPoint = transform(...)

```python
tPoint = transform(translations[i, :], ori, points=points[:, :3])
```

### Step 15: Assign mPoint = applyMatrix(...)

```python
mPoint = applyMatrix(m, points=points)
```

**Verification:**
```python
assert np.allclose(tPoint, mPoint[:, :3])
```


## Complete Example

```python
# Workflow
'Test if `transform` gives the same results as a matrix.'
np.random.seed(123456)
N = 1000
axes = np.random.uniform(-1.0, 1.0, (N, 3))
angles = np.random.uniform(0.0, 360.0, (N,))
translations = np.random.uniform(-10.0, 10.0, (N, 3))
points = np.zeros((N, 4))
points[:, :3] = np.random.uniform(-10.0, 10.0, (N, 3))
points[:, 3] = 1.0
for i in range(N):
    ori = quatFromAxisAngle(axes[i, :], angles[i], degrees=True)
    rm = rotationMatrix(angles[i], axes[i, :])
    tm = translationMatrix(translations[i, :])
    m = concatenate([rm, tm])
    tPoint = transform(translations[i, :], ori, points=points[:, :3])
    mPoint = applyMatrix(m, points=points)
    assert np.allclose(tPoint, mPoint[:, :3])
```

## Next Steps


---

*Source: test_mathtools.py:108 | Complexity: Advanced | Last updated: 2026-05-18*