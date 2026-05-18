# How To: Avscale Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AvScale outputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(average_scaling=dict(), backward_half_transform=dict(), determinant=dict(), forward_half_transform=dict(), left_right_orientation_preserved=dict(), rot_angles=dict(), rotation_translation_matrix=dict(), scales=dict(), skews=dict(), translations=dict())
```


## Complete Example

```python
# Workflow
output_map = dict(average_scaling=dict(), backward_half_transform=dict(), determinant=dict(), forward_half_transform=dict(), left_right_orientation_preserved=dict(), rot_angles=dict(), rotation_translation_matrix=dict(), scales=dict(), skews=dict(), translations=dict())
```

## Next Steps


---

*Source: test_auto_AvScale.py:36 | Complexity: Beginner | Last updated: 2026-05-18*