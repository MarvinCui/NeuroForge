# How To: Fitdwi Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FitDwi outputs

## Prerequisites

**Required Modules:**
- `dwi`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(error_file=dict(extensions=None), famap_file=dict(extensions=None), mcmap_file=dict(extensions=None), mcout=dict(extensions=None), mdmap_file=dict(extensions=None), nodiff_file=dict(extensions=None), res_file=dict(extensions=None), rgbmap_file=dict(extensions=None), syn_file=dict(extensions=None), tenmap2_file=dict(extensions=None), tenmap_file=dict(extensions=None), v1map_file=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(error_file=dict(extensions=None), famap_file=dict(extensions=None), mcmap_file=dict(extensions=None), mcout=dict(extensions=None), mdmap_file=dict(extensions=None), nodiff_file=dict(extensions=None), res_file=dict(extensions=None), rgbmap_file=dict(extensions=None), syn_file=dict(extensions=None), tenmap2_file=dict(extensions=None), tenmap_file=dict(extensions=None), v1map_file=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_FitDwi.py:281 | Complexity: Beginner | Last updated: 2026-05-18*