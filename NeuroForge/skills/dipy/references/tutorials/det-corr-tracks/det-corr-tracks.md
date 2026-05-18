# How To: Det Corr Tracks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test det corr tracks

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.tracking`


## Step-by-Step Guide

### Step 1: Assign A = np.array(...)

```python
A = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]])
```

**Verification:**
```python
assert_array_equal(arr, np.array([[0, 1], [1, 0]]))
```

### Step 2: Assign B = np.array(...)

```python
B = np.array([[1, 0, 0], [2, 0, 0], [3, 0, 0]])
```

**Verification:**
```python
assert_array_equal(arr, arr2)
```

### Step 3: Assign C = np.array(...)

```python
C = np.array([[0, 0, -1], [0, 0, -2], [0, 0, -3]])
```

### Step 4: Assign bundle1 = value

```python
bundle1 = [A, B, C]
```

### Step 5: Assign bundle2 = value

```python
bundle2 = [B, A]
```

### Step 6: Assign indices = value

```python
indices = [0, 1]
```

### Step 7: Call print()

```python
print(A)
```

### Step 8: Call print()

```python
print(B)
```

### Step 9: Call print()

```python
print(C)
```

### Step 10: Assign arr = tl.detect_corresponding_tracks(...)

```python
arr = tl.detect_corresponding_tracks(indices, bundle1, bundle2)
```

### Step 11: Call print()

```python
print(arr)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(arr, np.array([[0, 1], [1, 0]]))
```

### Step 13: Assign indices2 = value

```python
indices2 = [0, 1]
```

### Step 14: Assign arr2 = tl.detect_corresponding_tracks_plus(...)

```python
arr2 = tl.detect_corresponding_tracks_plus(indices, bundle1, indices2, bundle2)
```

### Step 15: Call print()

```python
print(arr2)
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(arr, arr2)
```


## Complete Example

```python
# Workflow
A = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]])
B = np.array([[1, 0, 0], [2, 0, 0], [3, 0, 0]])
C = np.array([[0, 0, -1], [0, 0, -2], [0, 0, -3]])
bundle1 = [A, B, C]
bundle2 = [B, A]
indices = [0, 1]
print(A)
print(B)
print(C)
arr = tl.detect_corresponding_tracks(indices, bundle1, bundle2)
print(arr)
assert_array_equal(arr, np.array([[0, 1], [1, 0]]))
indices2 = [0, 1]
arr2 = tl.detect_corresponding_tracks_plus(indices, bundle1, indices2, bundle2)
print(arr2)
assert_array_equal(arr, arr2)
```

## Next Steps


---

*Source: test_learning.py:9 | Complexity: Advanced | Last updated: 2026-05-18*