# How To: Brickstat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BrickStat inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None, position=2), max=dict(argstr='-max'), mean=dict(argstr='-mean'), min=dict(argstr='-min', position=1), percentile=dict(argstr='-percentile %.3f %.3f %.3f'), slow=dict(argstr='-slow'), sum=dict(argstr='-sum'), var=dict(argstr='-var'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None, position=2), max=dict(argstr='-max'), mean=dict(argstr='-mean'), min=dict(argstr='-min', position=1), percentile=dict(argstr='-percentile %.3f %.3f %.3f'), slow=dict(argstr='-slow'), sum=dict(argstr='-sum'), var=dict(argstr='-var'))
```

## Next Steps


---

*Source: test_auto_BrickStat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*