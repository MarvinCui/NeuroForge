# How To: Qualityindex Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test QualityIndex inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), autoclip=dict(argstr='-autoclip', usedefault=True, xor=['mask']), automask=dict(argstr='-automask', usedefault=True, xor=['mask']), clip=dict(argstr='-clip %f'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), interval=dict(argstr='-range', usedefault=True), mask=dict(argstr='-mask %s', extensions=None, xor=['autoclip', 'automask']), out_file=dict(argstr='> %s', extensions=None, keep_extension=False, name_source=['in_file'], name_template='%s_tqual', position=-1), quadrant=dict(argstr='-quadrant', usedefault=True), spearman=dict(argstr='-spearman', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), autoclip=dict(argstr='-autoclip', usedefault=True, xor=['mask']), automask=dict(argstr='-automask', usedefault=True, xor=['mask']), clip=dict(argstr='-clip %f'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), interval=dict(argstr='-range', usedefault=True), mask=dict(argstr='-mask %s', extensions=None, xor=['autoclip', 'automask']), out_file=dict(argstr='> %s', extensions=None, keep_extension=False, name_source=['in_file'], name_template='%s_tqual', position=-1), quadrant=dict(argstr='-quadrant', usedefault=True), spearman=dict(argstr='-spearman', usedefault=True))
```

## Next Steps


---

*Source: test_auto_QualityIndex.py:6 | Complexity: Beginner | Last updated: 2026-05-18*