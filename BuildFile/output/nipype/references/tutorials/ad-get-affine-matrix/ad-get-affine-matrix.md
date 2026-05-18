# How To: Ad Get Affine Matrix

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate reshape: test ad get affine matrix

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `interfaces.base`


## Step-by-Step Guide

### Step 1: Assign out = np.array.reshape(...)

```python
out = np.array([0, 0, 1, 0, 0, -1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1]).reshape((4, 4))
```


## Complete Example

```python
# Workflow
out = np.array([0, 0, 1, 0, 0, -1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1]).reshape((4, 4))
```

## Next Steps


---

*Source: test_rapidart.py:50 | Complexity: Beginner | Last updated: 2026-05-18*