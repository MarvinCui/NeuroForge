# How To: Bet Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BET outputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(inskull_mask_file=dict(extensions=None), inskull_mesh_file=dict(extensions=None), mask_file=dict(extensions=None), meshfile=dict(extensions=None), out_file=dict(extensions=None), outline_file=dict(extensions=None), outskin_mask_file=dict(extensions=None), outskin_mesh_file=dict(extensions=None), outskull_mask_file=dict(extensions=None), outskull_mesh_file=dict(extensions=None), skull_file=dict(extensions=None), skull_mask_file=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(inskull_mask_file=dict(extensions=None), inskull_mesh_file=dict(extensions=None), mask_file=dict(extensions=None), meshfile=dict(extensions=None), out_file=dict(extensions=None), outline_file=dict(extensions=None), outskin_mask_file=dict(extensions=None), outskin_mesh_file=dict(extensions=None), outskull_mask_file=dict(extensions=None), outskull_mesh_file=dict(extensions=None), skull_file=dict(extensions=None), skull_mask_file=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_BET.py:155 | Complexity: Beginner | Last updated: 2026-05-18*