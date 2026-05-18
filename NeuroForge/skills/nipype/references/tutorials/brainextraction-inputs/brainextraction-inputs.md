# How To: Brainextraction Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BrainExtraction inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(anatomical_image=dict(argstr='-a %s', extensions=None, mandatory=True), args=dict(argstr='%s'), brain_probability_mask=dict(argstr='-m %s', copyfile=False, extensions=None, mandatory=True), brain_template=dict(argstr='-e %s', extensions=None, mandatory=True), debug=dict(argstr='-z 1'), dimension=dict(argstr='-d %d', usedefault=True), environ=dict(nohash=True, usedefault=True), extraction_registration_mask=dict(argstr='-f %s', extensions=None), image_suffix=dict(argstr='-s %s', usedefault=True), keep_temporary_files=dict(argstr='-k %d'), num_threads=dict(nohash=True, usedefault=True), out_prefix=dict(argstr='-o %s', usedefault=True), use_floatingpoint_precision=dict(argstr='-q %d'), use_random_seeding=dict(argstr='-u %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(anatomical_image=dict(argstr='-a %s', extensions=None, mandatory=True), args=dict(argstr='%s'), brain_probability_mask=dict(argstr='-m %s', copyfile=False, extensions=None, mandatory=True), brain_template=dict(argstr='-e %s', extensions=None, mandatory=True), debug=dict(argstr='-z 1'), dimension=dict(argstr='-d %d', usedefault=True), environ=dict(nohash=True, usedefault=True), extraction_registration_mask=dict(argstr='-f %s', extensions=None), image_suffix=dict(argstr='-s %s', usedefault=True), keep_temporary_files=dict(argstr='-k %d'), num_threads=dict(nohash=True, usedefault=True), out_prefix=dict(argstr='-o %s', usedefault=True), use_floatingpoint_precision=dict(argstr='-q %d'), use_random_seeding=dict(argstr='-u %d'))
```

## Next Steps


---

*Source: test_auto_BrainExtraction.py:6 | Complexity: Beginner | Last updated: 2026-05-18*