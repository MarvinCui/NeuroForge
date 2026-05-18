# How To: Slicetimer Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SliceTimer inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), custom_order=dict(argstr='--ocustom=%s', extensions=None), custom_timings=dict(argstr='--tcustom=%s', extensions=None), environ=dict(nohash=True, usedefault=True), global_shift=dict(argstr='--tglobal'), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True, position=0), index_dir=dict(argstr='--down'), interleaved=dict(argstr='--odd'), out_file=dict(argstr='--out=%s', extensions=None, genfile=True, hash_files=False), output_type=dict(), slice_direction=dict(argstr='--direction=%d'), time_repetition=dict(argstr='--repeat=%f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), custom_order=dict(argstr='--ocustom=%s', extensions=None), custom_timings=dict(argstr='--tcustom=%s', extensions=None), environ=dict(nohash=True, usedefault=True), global_shift=dict(argstr='--tglobal'), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True, position=0), index_dir=dict(argstr='--down'), interleaved=dict(argstr='--odd'), out_file=dict(argstr='--out=%s', extensions=None, genfile=True, hash_files=False), output_type=dict(), slice_direction=dict(argstr='--direction=%d'), time_repetition=dict(argstr='--repeat=%f'))
```

## Next Steps


---

*Source: test_auto_SliceTimer.py:6 | Complexity: Beginner | Last updated: 2026-05-18*