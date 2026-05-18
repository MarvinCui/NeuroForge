# How To: Gtractinvertdisplacementfield Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractInvertDisplacementField inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), baseImage=dict(argstr='--baseImage %s', extensions=None), deformationImage=dict(argstr='--deformationImage %s', extensions=None), environ=dict(nohash=True, usedefault=True), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), subsamplingFactor=dict(argstr='--subsamplingFactor %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), baseImage=dict(argstr='--baseImage %s', extensions=None), deformationImage=dict(argstr='--deformationImage %s', extensions=None), environ=dict(nohash=True, usedefault=True), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), subsamplingFactor=dict(argstr='--subsamplingFactor %d'))
```

## Next Steps


---

*Source: test_auto_gtractInvertDisplacementField.py:6 | Complexity: Beginner | Last updated: 2026-05-18*