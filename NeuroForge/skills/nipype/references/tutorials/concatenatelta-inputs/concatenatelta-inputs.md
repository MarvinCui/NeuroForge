# How To: Concatenatelta Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ConcatenateLTA inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_lta1=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_lta2=dict(argstr='%s', mandatory=True, position=-2), invert_1=dict(argstr='-invert1'), invert_2=dict(argstr='-invert2'), invert_out=dict(argstr='-invertout'), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_lta1'], name_template='%s_concat', position=-1), out_type=dict(argstr='-out_type %d'), subject=dict(argstr='-subject %s'), subjects_dir=dict(), tal_source_file=dict(argstr='-tal %s', extensions=None, position=-5, requires=['tal_template_file']), tal_template_file=dict(argstr='%s', extensions=None, position=-4, requires=['tal_source_file']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_lta1=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_lta2=dict(argstr='%s', mandatory=True, position=-2), invert_1=dict(argstr='-invert1'), invert_2=dict(argstr='-invert2'), invert_out=dict(argstr='-invertout'), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_lta1'], name_template='%s_concat', position=-1), out_type=dict(argstr='-out_type %d'), subject=dict(argstr='-subject %s'), subjects_dir=dict(), tal_source_file=dict(argstr='-tal %s', extensions=None, position=-5, requires=['tal_template_file']), tal_template_file=dict(argstr='%s', extensions=None, position=-4, requires=['tal_source_file']))
```

## Next Steps


---

*Source: test_auto_ConcatenateLTA.py:6 | Complexity: Beginner | Last updated: 2026-05-18*