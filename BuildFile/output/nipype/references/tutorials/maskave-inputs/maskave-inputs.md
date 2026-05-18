# How To: Maskave Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Maskave inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), mask=dict(argstr='-mask %s', extensions=None, position=1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='> %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_maskave.1D', position=-1), outputtype=dict(), quiet=dict(argstr='-quiet', position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), mask=dict(argstr='-mask %s', extensions=None, position=1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='> %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_maskave.1D', position=-1), outputtype=dict(), quiet=dict(argstr='-quiet', position=2))
```

## Next Steps


---

*Source: test_auto_Maskave.py:6 | Complexity: Beginner | Last updated: 2026-05-18*