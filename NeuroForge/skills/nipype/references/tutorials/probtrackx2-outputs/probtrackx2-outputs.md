# How To: Probtrackx2 Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ProbTrackX2 outputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(fdt_paths=dict(), log=dict(extensions=None), lookup_tractspace=dict(extensions=None), matrix1_dot=dict(extensions=None), matrix2_dot=dict(extensions=None), matrix3_dot=dict(extensions=None), network_matrix=dict(extensions=None), particle_files=dict(), targets=dict(), way_total=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(fdt_paths=dict(), log=dict(extensions=None), lookup_tractspace=dict(extensions=None), matrix1_dot=dict(extensions=None), matrix2_dot=dict(extensions=None), matrix3_dot=dict(extensions=None), network_matrix=dict(extensions=None), particle_files=dict(), targets=dict(), way_total=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_ProbTrackX2.py:196 | Complexity: Beginner | Last updated: 2026-05-18*