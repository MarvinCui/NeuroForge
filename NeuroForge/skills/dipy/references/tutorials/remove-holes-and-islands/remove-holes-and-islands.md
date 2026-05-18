# How To: Remove Holes And Islands

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test remove holes and islands

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `dipy.segment.utils`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign temp = rng.choice(...)

```python
temp = rng.choice([0, 1], size=(40, 40, 40), p=[0.8, 0.2])
```

### Step 2: Assign unknown = 0

```python
temp[6:34, 6:34, 6:34] = 0
```

### Step 3: Assign unknown = 1

```python
temp[7:33, 7:33, 7:33] = 1
```

### Step 4: Assign unknown = rng.choice(...)

```python
temp[8:32, 8:32, 8:32] = rng.choice([0, 1], size=(24, 24, 24), p=[0.2, 0.8])
```

### Step 5: Assign output = remove_holes_and_islands(...)

```python
output = remove_holes_and_islands(temp)
```

### Step 6: Assign ground_truth = np.zeros(...)

```python
ground_truth = np.zeros((40, 40, 40))
```

### Step 7: Assign unknown = 1

```python
ground_truth[7:33, 7:33, 7:33] = 1
```

### Step 8: Call np.testing.assert_equal()

```python
np.testing.assert_equal(output, ground_truth)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
temp = rng.choice([0, 1], size=(40, 40, 40), p=[0.8, 0.2])
temp[6:34, 6:34, 6:34] = 0
temp[7:33, 7:33, 7:33] = 1
temp[8:32, 8:32, 8:32] = rng.choice([0, 1], size=(24, 24, 24), p=[0.2, 0.8])
output = remove_holes_and_islands(temp)
ground_truth = np.zeros((40, 40, 40))
ground_truth[7:33, 7:33, 7:33] = 1
np.testing.assert_equal(output, ground_truth)
```

## Next Steps


---

*Source: test_utils.py:9 | Complexity: Advanced | Last updated: 2026-05-18*