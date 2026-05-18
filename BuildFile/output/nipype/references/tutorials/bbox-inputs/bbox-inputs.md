# How To: Bbox Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BBox inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), format_minccrop=dict(argstr='-minccrop'), format_mincresample=dict(argstr='-mincresample'), format_mincreshape=dict(argstr='-mincreshape'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), one_line=dict(argstr='-one_line', xor=('one_line', 'two_lines')), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), output_file=dict(extensions=None, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s_bbox.txt', position=-1), threshold=dict(argstr='-threshold'), two_lines=dict(argstr='-two_lines', xor=('one_line', 'two_lines')))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), format_minccrop=dict(argstr='-minccrop'), format_mincresample=dict(argstr='-mincresample'), format_mincreshape=dict(argstr='-mincreshape'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), one_line=dict(argstr='-one_line', xor=('one_line', 'two_lines')), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), output_file=dict(extensions=None, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s_bbox.txt', position=-1), threshold=dict(argstr='-threshold'), two_lines=dict(argstr='-two_lines', xor=('one_line', 'two_lines')))
```

## Next Steps


---

*Source: test_auto_BBox.py:6 | Complexity: Beginner | Last updated: 2026-05-18*