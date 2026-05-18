# How To: Label2Label Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Label2Label inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='--hemi %s', mandatory=True), out_file=dict(argstr='--trglabel %s', extensions=None, hash_files=False, keep_extension=True, name_source=['source_label'], name_template='%s_converted'), registration_method=dict(argstr='--regmethod %s', usedefault=True), source_label=dict(argstr='--srclabel %s', extensions=None, mandatory=True), source_sphere_reg=dict(extensions=None, mandatory=True), source_subject=dict(argstr='--srcsubject %s', mandatory=True), source_white=dict(extensions=None, mandatory=True), sphere_reg=dict(extensions=None, mandatory=True), subject_id=dict(argstr='--trgsubject %s', mandatory=True, usedefault=True), subjects_dir=dict(), white=dict(extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='--hemi %s', mandatory=True), out_file=dict(argstr='--trglabel %s', extensions=None, hash_files=False, keep_extension=True, name_source=['source_label'], name_template='%s_converted'), registration_method=dict(argstr='--regmethod %s', usedefault=True), source_label=dict(argstr='--srclabel %s', extensions=None, mandatory=True), source_sphere_reg=dict(extensions=None, mandatory=True), source_subject=dict(argstr='--srcsubject %s', mandatory=True), source_white=dict(extensions=None, mandatory=True), sphere_reg=dict(extensions=None, mandatory=True), subject_id=dict(argstr='--trgsubject %s', mandatory=True, usedefault=True), subjects_dir=dict(), white=dict(extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_Label2Label.py:6 | Complexity: Beginner | Last updated: 2026-05-18*