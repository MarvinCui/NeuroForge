# How To: Computemeshwarp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ComputeMeshWarp inputs

## Prerequisites

**Required Modules:**
- `mesh`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(metric=dict(usedefault=True), out_file=dict(extensions=None, usedefault=True), out_warp=dict(extensions=None, usedefault=True), surface1=dict(extensions=None, mandatory=True), surface2=dict(extensions=None, mandatory=True), weighting=dict(usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(metric=dict(usedefault=True), out_file=dict(extensions=None, usedefault=True), out_warp=dict(extensions=None, usedefault=True), surface1=dict(extensions=None, mandatory=True), surface2=dict(extensions=None, mandatory=True), weighting=dict(usedefault=True))
```

## Next Steps


---

*Source: test_auto_ComputeMeshWarp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*