# How To: Computedvars Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ComputeDVARS outputs

## Prerequisites

**Required Modules:**
- `confounds`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(avg_nstd=dict(), avg_std=dict(), avg_vxstd=dict(), fig_nstd=dict(extensions=None), fig_std=dict(extensions=None), fig_vxstd=dict(extensions=None), out_all=dict(extensions=None), out_nstd=dict(extensions=None), out_std=dict(extensions=None), out_vxstd=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(avg_nstd=dict(), avg_std=dict(), avg_vxstd=dict(), fig_nstd=dict(extensions=None), fig_std=dict(extensions=None), fig_vxstd=dict(extensions=None), out_all=dict(extensions=None), out_nstd=dict(extensions=None), out_std=dict(extensions=None), out_vxstd=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_ComputeDVARS.py:58 | Complexity: Beginner | Last updated: 2026-05-18*