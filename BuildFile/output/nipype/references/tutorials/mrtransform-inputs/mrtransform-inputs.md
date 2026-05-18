# How To: Mrtransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRTransform inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), flip_x=dict(argstr='-flipx', position=1), in_files=dict(argstr='%s', mandatory=True, position=-2), invert=dict(argstr='-inverse', position=1), linear_transform=dict(argstr='-linear %s', extensions=None, position=1), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), quiet=dict(argstr='-quiet', position=1), reference_image=dict(argstr='-reference %s', extensions=None, position=1), replace_transform=dict(argstr='-replace', position=1), template_image=dict(argstr='-template %s', extensions=None, position=1), transformation_file=dict(argstr='-transform %s', extensions=None, position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), flip_x=dict(argstr='-flipx', position=1), in_files=dict(argstr='%s', mandatory=True, position=-2), invert=dict(argstr='-inverse', position=1), linear_transform=dict(argstr='-linear %s', extensions=None, position=1), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), quiet=dict(argstr='-quiet', position=1), reference_image=dict(argstr='-reference %s', extensions=None, position=1), replace_transform=dict(argstr='-replace', position=1), template_image=dict(argstr='-template %s', extensions=None, position=1), transformation_file=dict(argstr='-transform %s', extensions=None, position=1))
```

## Next Steps


---

*Source: test_auto_MRTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*