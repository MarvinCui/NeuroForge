# How To: Glm Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GLM outputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(out_cope=dict(), out_data=dict(), out_f=dict(), out_file=dict(extensions=None), out_p=dict(), out_pf=dict(), out_res=dict(), out_sigsq=dict(), out_t=dict(), out_varcb=dict(), out_vnscales=dict(), out_z=dict())
```


## Complete Example

```python
# Workflow
output_map = dict(out_cope=dict(), out_data=dict(), out_f=dict(), out_file=dict(extensions=None), out_p=dict(), out_pf=dict(), out_res=dict(), out_sigsq=dict(), out_t=dict(), out_varcb=dict(), out_vnscales=dict(), out_z=dict())
```

## Next Steps


---

*Source: test_auto_GLM.py:111 | Complexity: Beginner | Last updated: 2026-05-18*