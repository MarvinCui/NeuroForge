# How To: Mnibiascorrection Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MNIBiasCorrection inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), distance=dict(argstr='--distance %d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--i %s', extensions=None, mandatory=True), iterations=dict(argstr='--n %d', usedefault=True), mask=dict(argstr='--mask %s', extensions=None), no_rescale=dict(argstr='--no-rescale'), out_file=dict(argstr='--o %s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_output'), protocol_iterations=dict(argstr='--proto-iters %d'), shrink=dict(argstr='--shrink %d'), stop=dict(argstr='--stop %f'), subjects_dir=dict(), transform=dict(argstr='--uchar %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), distance=dict(argstr='--distance %d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--i %s', extensions=None, mandatory=True), iterations=dict(argstr='--n %d', usedefault=True), mask=dict(argstr='--mask %s', extensions=None), no_rescale=dict(argstr='--no-rescale'), out_file=dict(argstr='--o %s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_output'), protocol_iterations=dict(argstr='--proto-iters %d'), shrink=dict(argstr='--shrink %d'), stop=dict(argstr='--stop %f'), subjects_dir=dict(), transform=dict(argstr='--uchar %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_MNIBiasCorrection.py:6 | Complexity: Beginner | Last updated: 2026-05-18*