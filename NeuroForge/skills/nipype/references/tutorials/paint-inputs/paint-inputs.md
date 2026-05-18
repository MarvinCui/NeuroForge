# How To: Paint Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Paint inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), averages=dict(argstr='-a %d'), environ=dict(nohash=True, usedefault=True), in_surf=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_surf'], name_template='%s.avg_curv', position=-1), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-3), template_param=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), averages=dict(argstr='-a %d'), environ=dict(nohash=True, usedefault=True), in_surf=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_surf'], name_template='%s.avg_curv', position=-1), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-3), template_param=dict())
```

## Next Steps


---

*Source: test_auto_Paint.py:6 | Complexity: Beginner | Last updated: 2026-05-18*