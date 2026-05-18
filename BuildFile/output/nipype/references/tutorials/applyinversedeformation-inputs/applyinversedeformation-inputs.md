# How To: Applyinversedeformation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyInverseDeformation inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(bounding_box=dict(field='comp{1}.inv.comp{1}.sn2def.bb'), deformation=dict(extensions=None, field='comp{1}.inv.comp{1}.sn2def.matname', xor=['deformation_field']), deformation_field=dict(extensions=None, field='comp{1}.inv.comp{1}.def', xor=['deformation']), in_files=dict(field='fnames', mandatory=True), interpolation=dict(field='interp'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), target=dict(extensions=None, field='comp{1}.inv.space'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), voxel_sizes=dict(field='comp{1}.inv.comp{1}.sn2def.vox'))
```


## Complete Example

```python
# Workflow
input_map = dict(bounding_box=dict(field='comp{1}.inv.comp{1}.sn2def.bb'), deformation=dict(extensions=None, field='comp{1}.inv.comp{1}.sn2def.matname', xor=['deformation_field']), deformation_field=dict(extensions=None, field='comp{1}.inv.comp{1}.def', xor=['deformation']), in_files=dict(field='fnames', mandatory=True), interpolation=dict(field='interp'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), target=dict(extensions=None, field='comp{1}.inv.space'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), voxel_sizes=dict(field='comp{1}.inv.comp{1}.sn2def.vox'))
```

## Next Steps


---

*Source: test_auto_ApplyInverseDeformation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*