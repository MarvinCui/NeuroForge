# How To: Visualangle

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test visual angle calculation.

This tests the visual angle calculation for a few values. The test is
performed by converting the visual angle back to a distance and checking if
it is the same as the original distance.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test visual angle calculation.\n\n    This tests the visual angle calculation for a few values. The test is\n    performed by converting the visual angle back to a distance and checking if\n    it is the same as the original distance.\n\n    '

```python
'Test visual angle calculation.\n\n    This tests the visual angle calculation for a few values. The test is\n    performed by converting the visual angle back to a distance and checking if\n    it is the same as the original distance.\n\n    '
```

**Verification:**
```python
assert np.isclose(visualAngle(0.01, 0.57), 1.0051633)
```

### Step 2: Assign N = 1000

```python
N = 1000
```

**Verification:**
```python
assert np.all(a <= 180) and np.all(b <= 180) and np.all(c <= 180)
```

### Step 3: Call np.random.seed()

```python
np.random.seed(12345)
```

**Verification:**
```python
assert np.all(a >= 0) and np.all(b >= 0) and np.all(c >= 0)
```

### Step 4: Assign distances = np.random.uniform(...)

```python
distances = np.random.uniform(0.1, 100.0, (N,))
```

### Step 5: Assign sizes = np.random.uniform(...)

```python
sizes = np.random.uniform(0.01, 10.0, (N,))
```

### Step 6: Assign a = visualAngle(...)

```python
a = visualAngle(sizes, distances)
```

### Step 7: Assign b = visualAngle(...)

```python
b = visualAngle(sizes, 0.57)
```

### Step 8: Assign c = visualAngle(...)

```python
c = visualAngle(1.0, distances)
```

**Verification:**
```python
assert np.all(a <= 180) and np.all(b <= 180) and np.all(c <= 180)
```


## Complete Example

```python
# Workflow
'Test visual angle calculation.\n\n    This tests the visual angle calculation for a few values. The test is\n    performed by converting the visual angle back to a distance and checking if\n    it is the same as the original distance.\n\n    '
assert np.isclose(visualAngle(0.01, 0.57), 1.0051633)
N = 1000
np.random.seed(12345)
distances = np.random.uniform(0.1, 100.0, (N,))
sizes = np.random.uniform(0.01, 10.0, (N,))
a = visualAngle(sizes, distances)
b = visualAngle(sizes, 0.57)
c = visualAngle(1.0, distances)
assert np.all(a <= 180) and np.all(b <= 180) and np.all(c <= 180)
assert np.all(a >= 0) and np.all(b >= 0) and np.all(c >= 0)
```

## Next Steps


---

*Source: test_viewtools.py:12 | Complexity: Advanced | Last updated: 2026-05-18*