# How To: Watershedbem Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WatershedBEM outputs

## Prerequisites

**Required Modules:**
- `base`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(brain_surface=dict(extensions=None, loc='bem/watershed'), cor_files=dict(altkey='COR', loc='bem/watershed/ws'), fif_file=dict(altkey='fif', extensions=None, loc='bem'), inner_skull_surface=dict(extensions=None, loc='bem/watershed'), mesh_files=dict(), outer_skin_surface=dict(extensions=None, loc='bem/watershed'), outer_skull_surface=dict(extensions=None, loc='bem/watershed'))
```


## Complete Example

```python
# Workflow
output_map = dict(brain_surface=dict(extensions=None, loc='bem/watershed'), cor_files=dict(altkey='COR', loc='bem/watershed/ws'), fif_file=dict(altkey='fif', extensions=None, loc='bem'), inner_skull_surface=dict(extensions=None, loc='bem/watershed'), mesh_files=dict(), outer_skin_surface=dict(extensions=None, loc='bem/watershed'), outer_skull_surface=dict(extensions=None, loc='bem/watershed'))
```

## Next Steps


---

*Source: test_auto_WatershedBEM.py:42 | Complexity: Beginner | Last updated: 2026-05-18*