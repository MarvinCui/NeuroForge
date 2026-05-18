# How To: Surfacetransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SurfaceTransform inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), hemi=dict(argstr='--hemi %s', mandatory=True), out_file=dict(argstr='--tval %s', extensions=None, genfile=True), reshape=dict(argstr='--reshape'), reshape_factor=dict(argstr='--reshape-factor'), source_annot_file=dict(argstr='--sval-annot %s', extensions=None, mandatory=True, xor=['source_file']), source_file=dict(argstr='--sval %s', extensions=None, mandatory=True, xor=['source_annot_file']), source_subject=dict(argstr='--srcsubject %s', mandatory=True), source_type=dict(argstr='--sfmt %s', requires=['source_file']), subjects_dir=dict(), target_ico_order=dict(argstr='--trgicoorder %d'), target_subject=dict(argstr='--trgsubject %s', mandatory=True), target_type=dict(argstr='--tfmt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), hemi=dict(argstr='--hemi %s', mandatory=True), out_file=dict(argstr='--tval %s', extensions=None, genfile=True), reshape=dict(argstr='--reshape'), reshape_factor=dict(argstr='--reshape-factor'), source_annot_file=dict(argstr='--sval-annot %s', extensions=None, mandatory=True, xor=['source_file']), source_file=dict(argstr='--sval %s', extensions=None, mandatory=True, xor=['source_annot_file']), source_subject=dict(argstr='--srcsubject %s', mandatory=True), source_type=dict(argstr='--sfmt %s', requires=['source_file']), subjects_dir=dict(), target_ico_order=dict(argstr='--trgicoorder %d'), target_subject=dict(argstr='--trgsubject %s', mandatory=True), target_type=dict(argstr='--tfmt %s'))
```

## Next Steps


---

*Source: test_auto_SurfaceTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*