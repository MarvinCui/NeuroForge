# How To: Extractroibasedsurfacemeasures Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ExtractROIBasedSurfaceMeasures inputs

## Prerequisites

**Required Modules:**
- `surface`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(lh_roi_atlas=dict(copyfile=False, field='rdata', mandatory=True), lh_surface_measure=dict(copyfile=False, field='cdata', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), rh_roi_atlas=dict(copyfile=False, mandatory=False), rh_surface_measure=dict(copyfile=False, mandatory=False), surface_files=dict(copyfile=False, mandatory=False), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(lh_roi_atlas=dict(copyfile=False, field='rdata', mandatory=True), lh_surface_measure=dict(copyfile=False, field='cdata', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), rh_roi_atlas=dict(copyfile=False, mandatory=False), rh_surface_measure=dict(copyfile=False, mandatory=False), surface_files=dict(copyfile=False, mandatory=False), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_ExtractROIBasedSurfaceMeasures.py:6 | Complexity: Beginner | Last updated: 2026-05-18*