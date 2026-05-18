# How To: Denoiseimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DenoiseImage inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='-d %d'), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='-i %s', extensions=None, mandatory=True), noise_image=dict(extensions=None, hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_noise'), noise_model=dict(argstr='-n %s', usedefault=True), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='-o %s', extensions=None, hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_noise_corrected'), save_noise=dict(mandatory=True, usedefault=True, xor=['noise_image']), shrink_factor=dict(argstr='-s %s', usedefault=True), verbose=dict(argstr='-v'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='-d %d'), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='-i %s', extensions=None, mandatory=True), noise_image=dict(extensions=None, hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_noise'), noise_model=dict(argstr='-n %s', usedefault=True), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='-o %s', extensions=None, hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_noise_corrected'), save_noise=dict(mandatory=True, usedefault=True, xor=['noise_image']), shrink_factor=dict(argstr='-s %s', usedefault=True), verbose=dict(argstr='-v'))
```

## Next Steps


---

*Source: test_auto_DenoiseImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*