# How To: Reorder Labels

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: When labels have non-consecutive integers, make them consecutive by     reordering them to make no gaps/differences between integers.

We expect labels to be of same shape even if they are reordered.

Issue #938, comment #14.

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

### Step 1: 'When labels have non-consecutive integers, make them consecutive by     reordering them to make no gaps/differences between integers.\n\n    We expect labels to be of same shape even if they are reordered.\n\n    Issue #938, comment #14.\n    '

```python
'When labels have non-consecutive integers, make them consecutive by     reordering them to make no gaps/differences between integers.\n\n    We expect labels to be of same shape even if they are reordered.\n\n    Issue #938, comment #14.\n    '
```

**Verification:**
```python
assert data.shape == labels.shape
```

### Step 2: Assign data = value

```python
data = np.zeros((5, 5)) + 0.1 * rng.standard_normal(size=(5, 5))
```

### Step 3: Assign unknown = 1

```python
data[1:5, 1:5] = 1
```

### Step 4: Assign labels = np.zeros_like(...)

```python
labels = np.zeros_like(data)
```

### Step 5: Assign unknown = 1

```python
labels[3, 3] = 1
```

### Step 6: Assign unknown = 4

```python
labels[1, 4] = 4
```

### Step 7: Assign labels = random_walker(...)

```python
labels = random_walker(data, labels)
```

**Verification:**
```python
assert data.shape == labels.shape
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'When labels have non-consecutive integers, make them consecutive by     reordering them to make no gaps/differences between integers.\n\n    We expect labels to be of same shape even if they are reordered.\n\n    Issue #938, comment #14.\n    '
data = np.zeros((5, 5)) + 0.1 * rng.standard_normal(size=(5, 5))
data[1:5, 1:5] = 1
labels = np.zeros_like(data)
labels[3, 3] = 1
labels[1, 4] = 4
labels = random_walker(data, labels)
assert data.shape == labels.shape
```

## Next Steps


---

*Source: test_segmentation.py:127 | Complexity: Intermediate | Last updated: 2026-05-18*