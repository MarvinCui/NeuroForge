# How To: Epireg Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EpiReg outputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(epi2str_inv=dict(extensions=None), epi2str_mat=dict(extensions=None), fmap2epi_mat=dict(extensions=None), fmap2str_mat=dict(extensions=None), fmap_epi=dict(extensions=None), fmap_str=dict(extensions=None), fmapmag_str=dict(extensions=None), fullwarp=dict(extensions=None), out_1vol=dict(extensions=None), out_file=dict(extensions=None), seg=dict(extensions=None), shiftmap=dict(extensions=None), wmedge=dict(extensions=None), wmseg=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(epi2str_inv=dict(extensions=None), epi2str_mat=dict(extensions=None), fmap2epi_mat=dict(extensions=None), fmap2str_mat=dict(extensions=None), fmap_epi=dict(extensions=None), fmap_str=dict(extensions=None), fmapmag_str=dict(extensions=None), fullwarp=dict(extensions=None), out_1vol=dict(extensions=None), out_file=dict(extensions=None), seg=dict(extensions=None), shiftmap=dict(extensions=None), wmedge=dict(extensions=None), wmseg=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_EpiReg.py:80 | Complexity: Beginner | Last updated: 2026-05-18*