# How To: Remove Holes And Islands Warnings

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate concatenate: test remove holes and islands warnings

## Prerequisites

**Required Modules:**
- `numpy`
- `dipy.segment.utils`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign non_binary_img = np.concatenate(...)

```python
non_binary_img = np.concatenate([np.zeros((30, 30, 10)), np.ones((30, 30, 10)), np.ones((30, 30, 10)) * 2], axis=-1)
```


## Complete Example

```python
# Workflow
non_binary_img = np.concatenate([np.zeros((30, 30, 10)), np.ones((30, 30, 10)), np.ones((30, 30, 10)) * 2], axis=-1)
```

## Next Steps


---

*Source: test_utils.py:22 | Complexity: Beginner | Last updated: 2026-05-18*