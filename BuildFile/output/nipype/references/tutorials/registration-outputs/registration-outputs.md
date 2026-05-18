# How To: Registration Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Registration outputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(composite_transform=dict(extensions=None), elapsed_time=dict(), forward_invert_flags=dict(), forward_transforms=dict(), inverse_composite_transform=dict(extensions=None), inverse_warped_image=dict(extensions=None), metric_value=dict(), reverse_forward_invert_flags=dict(), reverse_forward_transforms=dict(), reverse_invert_flags=dict(), reverse_transforms=dict(), save_state=dict(extensions=None), warped_image=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(composite_transform=dict(extensions=None), elapsed_time=dict(), forward_invert_flags=dict(), forward_transforms=dict(), inverse_composite_transform=dict(extensions=None), inverse_warped_image=dict(extensions=None), metric_value=dict(), reverse_forward_invert_flags=dict(), reverse_forward_transforms=dict(), reverse_invert_flags=dict(), reverse_transforms=dict(), save_state=dict(extensions=None), warped_image=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_Registration.py:185 | Complexity: Beginner | Last updated: 2026-05-18*