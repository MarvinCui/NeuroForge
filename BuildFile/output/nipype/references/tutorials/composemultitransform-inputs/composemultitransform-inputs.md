# How To: Composemultitransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ComposeMultiTransform inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), output_transform=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['transforms'], name_template='%s_composed', position=1), reference_image=dict(argstr='%s', extensions=None, position=2), transforms=dict(argstr='%s', mandatory=True, position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), output_transform=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['transforms'], name_template='%s_composed', position=1), reference_image=dict(argstr='%s', extensions=None, position=2), transforms=dict(argstr='%s', mandatory=True, position=3))
```

## Next Steps


---

*Source: test_auto_ComposeMultiTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*