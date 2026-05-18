# How To: Remlfit Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Remlfit outputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(errts_file=dict(extensions=None), fitts_file=dict(extensions=None), glt_file=dict(extensions=None), obeta=dict(extensions=None), obuck=dict(extensions=None), oerrts=dict(extensions=None), ofitts=dict(extensions=None), oglt=dict(extensions=None), out_file=dict(extensions=None), ovar=dict(extensions=None), rbeta_file=dict(extensions=None), var_file=dict(extensions=None), wherr_file=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(errts_file=dict(extensions=None), fitts_file=dict(extensions=None), glt_file=dict(extensions=None), obeta=dict(extensions=None), obuck=dict(extensions=None), oerrts=dict(extensions=None), ofitts=dict(extensions=None), oglt=dict(extensions=None), out_file=dict(extensions=None), ovar=dict(extensions=None), rbeta_file=dict(extensions=None), var_file=dict(extensions=None), wherr_file=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_Remlfit.py:166 | Complexity: Beginner | Last updated: 2026-05-18*