# How To: Xfminvert Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test XfmInvert inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), verbose=dict(argstr='-verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), verbose=dict(argstr='-verbose'))
```

## Next Steps


---

*Source: test_auto_XfmInvert.py:6 | Complexity: Beginner | Last updated: 2026-05-18*