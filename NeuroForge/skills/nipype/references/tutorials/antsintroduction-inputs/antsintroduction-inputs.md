# How To: Antsintroduction Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test antsIntroduction inputs

## Prerequisites

**Required Modules:**
- `legacy`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bias_field_correction=dict(argstr='-n 1'), dimension=dict(argstr='-d %d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), force_proceed=dict(argstr='-f 1'), input_image=dict(argstr='-i %s', copyfile=False, extensions=None, mandatory=True), inverse_warp_template_labels=dict(argstr='-l'), max_iterations=dict(argstr='-m %s', sep='x'), num_threads=dict(nohash=True, usedefault=True), out_prefix=dict(argstr='-o %s', usedefault=True), quality_check=dict(argstr='-q 1'), reference_image=dict(argstr='-r %s', copyfile=True, extensions=None, mandatory=True), similarity_metric=dict(argstr='-s %s'), transformation_model=dict(argstr='-t %s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bias_field_correction=dict(argstr='-n 1'), dimension=dict(argstr='-d %d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), force_proceed=dict(argstr='-f 1'), input_image=dict(argstr='-i %s', copyfile=False, extensions=None, mandatory=True), inverse_warp_template_labels=dict(argstr='-l'), max_iterations=dict(argstr='-m %s', sep='x'), num_threads=dict(nohash=True, usedefault=True), out_prefix=dict(argstr='-o %s', usedefault=True), quality_check=dict(argstr='-q 1'), reference_image=dict(argstr='-r %s', copyfile=True, extensions=None, mandatory=True), similarity_metric=dict(argstr='-s %s'), transformation_model=dict(argstr='-t %s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_antsIntroduction.py:6 | Complexity: Beginner | Last updated: 2026-05-18*