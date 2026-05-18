# How To: Mrifill Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIFill inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), log_file=dict(argstr='-a %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), segmentation=dict(argstr='-segmentation %s', extensions=None), subjects_dir=dict(), transform=dict(argstr='-xform %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), log_file=dict(argstr='-a %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), segmentation=dict(argstr='-segmentation %s', extensions=None), subjects_dir=dict(), transform=dict(argstr='-xform %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_MRIFill.py:6 | Complexity: Beginner | Last updated: 2026-05-18*