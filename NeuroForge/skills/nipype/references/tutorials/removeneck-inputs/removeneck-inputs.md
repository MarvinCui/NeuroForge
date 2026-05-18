# How To: Removeneck Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RemoveNeck inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_noneck', position=-1), radius=dict(argstr='-radius %d'), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-2), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_noneck', position=-1), radius=dict(argstr='-radius %d'), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-2), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-3))
```

## Next Steps


---

*Source: test_auto_RemoveNeck.py:6 | Complexity: Beginner | Last updated: 2026-05-18*