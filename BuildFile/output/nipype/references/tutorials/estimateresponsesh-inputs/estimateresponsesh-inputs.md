# How To: Estimateresponsesh Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EstimateResponseSH inputs

## Prerequisites

**Required Modules:**
- `reconstruction`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(auto=dict(xor=['recursive']), b0_thres=dict(usedefault=True), fa_thresh=dict(usedefault=True), in_bval=dict(extensions=None, mandatory=True), in_bvec=dict(extensions=None, mandatory=True), in_evals=dict(extensions=None, mandatory=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None), out_mask=dict(extensions=None, usedefault=True), out_prefix=dict(), recursive=dict(xor=['auto']), response=dict(extensions=None, usedefault=True), roi_radius=dict(usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(auto=dict(xor=['recursive']), b0_thres=dict(usedefault=True), fa_thresh=dict(usedefault=True), in_bval=dict(extensions=None, mandatory=True), in_bvec=dict(extensions=None, mandatory=True), in_evals=dict(extensions=None, mandatory=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None), out_mask=dict(extensions=None, usedefault=True), out_prefix=dict(), recursive=dict(xor=['auto']), response=dict(extensions=None, usedefault=True), roi_radius=dict(usedefault=True))
```

## Next Steps


---

*Source: test_auto_EstimateResponseSH.py:6 | Complexity: Beginner | Last updated: 2026-05-18*