# How To: Separable Data Is Inside Radius

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test separable data is inside radius

## Prerequisites

**Required Modules:**
- `_tools`
- `svm`


## Step-by-Step Guide

### Step 1: Assign positions = value

```python
positions = [[(1, 1), (-1, -1)], [(1, 1, 10), (100, -20, 30), (-1, 10, 1000)]]
```

**Verification:**
```python
assert rad ** 2 > _sqdist(pos[idx], d)
```

### Step 2: Assign labels = value

```python
labels = [[1, -1], [1, 2, 3]]
```

### Step 3: Assign radii = value

```python
radii = [0.5, 1, 10]
```

### Step 4: Assign num_elem = 100

```python
num_elem = 100
```

### Step 5: Assign unknown = _separable_data(...)

```python
data, ls = _separable_data(pos, labs, rad, num_elem)
```

### Step 6: Assign idx = labs.index(...)

```python
idx = labs.index(l)
```

**Verification:**
```python
assert rad ** 2 > _sqdist(pos[idx], d)
```


## Complete Example

```python
# Workflow
positions = [[(1, 1), (-1, -1)], [(1, 1, 10), (100, -20, 30), (-1, 10, 1000)]]
labels = [[1, -1], [1, 2, 3]]
radii = [0.5, 1, 10]
num_elem = 100
for pos, labs in zip(positions, labels):
    for rad in radii:
        data, ls = _separable_data(pos, labs, rad, num_elem)
        for d, l in zip(data, ls):
            idx = labs.index(l)
            assert rad ** 2 > _sqdist(pos[idx], d)
```

## Next Steps


---

*Source: test_svm_classifier.py:65 | Complexity: Intermediate | Last updated: 2026-05-18*