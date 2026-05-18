# How To: Averageimages Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AverageImages inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), images=dict(argstr='%s', mandatory=True, position=3), normalize=dict(argstr='%d', mandatory=True, position=2), num_threads=dict(nohash=True, usedefault=True), output_average_image=dict(argstr='%s', extensions=None, hash_files=False, position=1, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), images=dict(argstr='%s', mandatory=True, position=3), normalize=dict(argstr='%d', mandatory=True, position=2), num_threads=dict(nohash=True, usedefault=True), output_average_image=dict(argstr='%s', extensions=None, hash_files=False, position=1, usedefault=True))
```

## Next Steps


---

*Source: test_auto_AverageImages.py:6 | Complexity: Beginner | Last updated: 2026-05-18*