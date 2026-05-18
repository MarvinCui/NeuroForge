# How To: Isolated Seed

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test isolated seed

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn._utils.segmentation`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign data = rng.random(...)

```python
data = rng.random((3, 3))
```

### Step 2: Assign labels = value

```python
labels = -np.ones((3, 3))
```

### Step 3: Assign unknown = 1

```python
labels[0, 1] = 1
```

### Step 4: Assign unknown = 0

```python
labels[0, 0] = 0
```

### Step 5: Assign unknown = 2

```python
labels[2, 2] = 2
```

### Step 6: Assign expected = np.array(...)

```python
expected = np.array([[1.0, 1.0, -1.0], [-1.0, -1.0, -1.0], [-1.0, -1.0, -1.0]])
```

### Step 7: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(expected, random_walker(data, labels))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
data = rng.random((3, 3))
labels = -np.ones((3, 3))
labels[0, 1] = 1
labels[0, 0] = 0
labels[2, 2] = 2
expected = np.array([[1.0, 1.0, -1.0], [-1.0, -1.0, -1.0], [-1.0, -1.0, -1.0]])
np.testing.assert_array_equal(expected, random_walker(data, labels))
```

## Next Steps


---

*Source: test_segmentation.py:59 | Complexity: Intermediate | Last updated: 2026-05-18*