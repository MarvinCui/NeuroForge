# How To: Createwarped Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CreateWarped inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(flowfield_files=dict(copyfile=False, field='crt_warped.flowfields', mandatory=True), image_files=dict(copyfile=False, field='crt_warped.images', mandatory=True), interp=dict(field='crt_warped.interp'), iterations=dict(field='crt_warped.K'), matlab_cmd=dict(), mfile=dict(usedefault=True), modulate=dict(field='crt_warped.jactransf'), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(flowfield_files=dict(copyfile=False, field='crt_warped.flowfields', mandatory=True), image_files=dict(copyfile=False, field='crt_warped.images', mandatory=True), interp=dict(field='crt_warped.interp'), iterations=dict(field='crt_warped.K'), matlab_cmd=dict(), mfile=dict(usedefault=True), modulate=dict(field='crt_warped.jactransf'), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_CreateWarped.py:6 | Complexity: Beginner | Last updated: 2026-05-18*