# How To: Registeravitotalairach Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RegisterAVItoTalairach inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, position=3, usedefault=True), subjects_dir=dict(), target=dict(argstr='%s', extensions=None, mandatory=True, position=1), vox2vox=dict(argstr='%s', extensions=None, mandatory=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, position=3, usedefault=True), subjects_dir=dict(), target=dict(argstr='%s', extensions=None, mandatory=True, position=1), vox2vox=dict(argstr='%s', extensions=None, mandatory=True, position=2))
```

## Next Steps


---

*Source: test_auto_RegisterAVItoTalairach.py:6 | Complexity: Beginner | Last updated: 2026-05-18*