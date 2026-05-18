# How To: Extractadditionalsurfaceparameters Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ExtractAdditionalSurfaceParameters inputs

## Prerequisites

**Required Modules:**
- `surface`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(area=dict(field='area', usedefault=True), depth=dict(field='SD', usedefault=True), fractal_dimension=dict(field='FD', usedefault=True), gmv=dict(field='gmv', usedefault=True), gyrification=dict(field='GI', usedefault=True), left_central_surfaces=dict(copyfile=False, field='data_surf', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), surface_files=dict(copyfile=False, mandatory=False), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(area=dict(field='area', usedefault=True), depth=dict(field='SD', usedefault=True), fractal_dimension=dict(field='FD', usedefault=True), gmv=dict(field='gmv', usedefault=True), gyrification=dict(field='GI', usedefault=True), left_central_surfaces=dict(copyfile=False, field='data_surf', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), surface_files=dict(copyfile=False, mandatory=False), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_ExtractAdditionalSurfaceParameters.py:6 | Complexity: Beginner | Last updated: 2026-05-18*