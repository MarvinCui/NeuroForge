# How To: Mrisinflate Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIsInflate inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), no_save_sulc=dict(argstr='-no-save-sulc', xor=['out_sulc']), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s.inflated', position=-1), out_sulc=dict(extensions=None, xor=['no_save_sulc']), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), no_save_sulc=dict(argstr='-no-save-sulc', xor=['out_sulc']), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s.inflated', position=-1), out_sulc=dict(extensions=None, xor=['no_save_sulc']), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_MRIsInflate.py:6 | Complexity: Beginner | Last updated: 2026-05-18*