# How To: Csd Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CSD inputs

## Prerequisites

**Required Modules:**
- `reconstruction`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(b0_thres=dict(usedefault=True), in_bval=dict(extensions=None, mandatory=True), in_bvec=dict(extensions=None, mandatory=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None), out_fods=dict(extensions=None), out_prefix=dict(), response=dict(extensions=None), save_fods=dict(usedefault=True), sh_order=dict(usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(b0_thres=dict(usedefault=True), in_bval=dict(extensions=None, mandatory=True), in_bvec=dict(extensions=None, mandatory=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None), out_fods=dict(extensions=None), out_prefix=dict(), response=dict(extensions=None), save_fods=dict(usedefault=True), sh_order=dict(usedefault=True))
```

## Next Steps


---

*Source: test_auto_CSD.py:6 | Complexity: Beginner | Last updated: 2026-05-18*