# How To: Robexsegment Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RobexSegment inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_brain', position=1), out_mask=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_brainmask', position=2), seed=dict(argstr='%i', position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_brain', position=1), out_mask=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_brainmask', position=2), seed=dict(argstr='%i', position=3))
```

## Next Steps


---

*Source: test_auto_RobexSegment.py:6 | Complexity: Beginner | Last updated: 2026-05-18*