# How To: Cartesian

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate array: test cartesian

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc.math`
- `pymc.pytensorf`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign manual_cartesian = np.array(...)

```python
manual_cartesian = np.array([[1, 0, 5], [1, 0, 6], [1, 2, 5], [1, 2, 6], [2, 0, 5], [2, 0, 6], [2, 2, 5], [2, 2, 6], [3, 0, 5], [3, 0, 6], [3, 2, 5], [3, 2, 6]])
```


## Complete Example

```python
# Workflow
manual_cartesian = np.array([[1, 0, 5], [1, 0, 6], [1, 2, 5], [1, 2, 6], [2, 0, 5], [2, 0, 6], [2, 2, 5], [2, 2, 6], [3, 0, 5], [3, 0, 6], [3, 2, 5], [3, 2, 6]])
```

## Next Steps


---

*Source: test_math.py:53 | Complexity: Beginner | Last updated: 2026-05-18*