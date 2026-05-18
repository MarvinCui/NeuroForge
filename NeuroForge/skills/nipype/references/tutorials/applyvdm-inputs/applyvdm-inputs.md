# How To: Applyvdm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyVDM inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(distortion_direction=dict(field='roptions.pedir', usedefault=True), in_files=dict(copyfile=True, field='data.scans', mandatory=True), interpolation=dict(field='roptions.rinterp'), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='roptions.prefix', usedefault=True), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), vdmfile=dict(copyfile=True, extensions=None, field='data.vdmfile', mandatory=True), write_mask=dict(field='roptions.mask'), write_which=dict(field='roptions.which', usedefault=True), write_wrap=dict(field='roptions.wrap'))
```


## Complete Example

```python
# Workflow
input_map = dict(distortion_direction=dict(field='roptions.pedir', usedefault=True), in_files=dict(copyfile=True, field='data.scans', mandatory=True), interpolation=dict(field='roptions.rinterp'), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='roptions.prefix', usedefault=True), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), vdmfile=dict(copyfile=True, extensions=None, field='data.vdmfile', mandatory=True), write_mask=dict(field='roptions.mask'), write_which=dict(field='roptions.which', usedefault=True), write_wrap=dict(field='roptions.wrap'))
```

## Next Steps


---

*Source: test_auto_ApplyVDM.py:6 | Complexity: Beginner | Last updated: 2026-05-18*