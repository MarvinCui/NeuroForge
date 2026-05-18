# How To: Dtirecon Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DTIRecon outputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(ADC=dict(extensions=None), B0=dict(extensions=None), FA=dict(extensions=None), FA_color=dict(extensions=None), L1=dict(extensions=None), L2=dict(extensions=None), L3=dict(extensions=None), V1=dict(extensions=None), V2=dict(extensions=None), V3=dict(extensions=None), exp=dict(extensions=None), tensor=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(ADC=dict(extensions=None), B0=dict(extensions=None), FA=dict(extensions=None), FA_color=dict(extensions=None), L1=dict(extensions=None), L2=dict(extensions=None), L3=dict(extensions=None), V1=dict(extensions=None), V2=dict(extensions=None), V3=dict(extensions=None), exp=dict(extensions=None), tensor=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_DTIRecon.py:59 | Complexity: Beginner | Last updated: 2026-05-18*