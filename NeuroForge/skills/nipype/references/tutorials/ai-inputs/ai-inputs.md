# How To: Ai Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AI inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), convergence=dict(argstr='-c [%d,%g,%d]', usedefault=True), dimension=dict(argstr='-d %d', usedefault=True), environ=dict(nohash=True, usedefault=True), fixed_image=dict(extensions=None, mandatory=True), fixed_image_mask=dict(argstr='-x %s', extensions=None), metric=dict(argstr='-m %s', mandatory=True), moving_image=dict(extensions=None, mandatory=True), moving_image_mask=dict(extensions=None, requires=['fixed_image_mask']), num_threads=dict(nohash=True, usedefault=True), output_transform=dict(argstr='-o %s', extensions=None, usedefault=True), principal_axes=dict(argstr='-p %d', usedefault=True, xor=['blobs']), search_factor=dict(argstr='-s [%g,%g]', usedefault=True), search_grid=dict(argstr='-g %s', min_ver='2.3.0'), transform=dict(argstr='-t %s[%g]', usedefault=True), verbose=dict(argstr='-v %d', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), convergence=dict(argstr='-c [%d,%g,%d]', usedefault=True), dimension=dict(argstr='-d %d', usedefault=True), environ=dict(nohash=True, usedefault=True), fixed_image=dict(extensions=None, mandatory=True), fixed_image_mask=dict(argstr='-x %s', extensions=None), metric=dict(argstr='-m %s', mandatory=True), moving_image=dict(extensions=None, mandatory=True), moving_image_mask=dict(extensions=None, requires=['fixed_image_mask']), num_threads=dict(nohash=True, usedefault=True), output_transform=dict(argstr='-o %s', extensions=None, usedefault=True), principal_axes=dict(argstr='-p %d', usedefault=True, xor=['blobs']), search_factor=dict(argstr='-s [%g,%g]', usedefault=True), search_grid=dict(argstr='-g %s', min_ver='2.3.0'), transform=dict(argstr='-t %s[%g]', usedefault=True), verbose=dict(argstr='-v %d', usedefault=True))
```

## Next Steps


---

*Source: test_auto_AI.py:6 | Complexity: Beginner | Last updated: 2026-05-18*