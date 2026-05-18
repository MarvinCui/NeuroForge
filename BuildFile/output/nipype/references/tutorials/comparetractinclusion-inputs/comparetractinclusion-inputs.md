# How To: Comparetractinclusion Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test compareTractInclusion inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), closeness=dict(argstr='--closeness %f'), environ=dict(nohash=True, usedefault=True), numberOfPoints=dict(argstr='--numberOfPoints %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), standardFiber=dict(argstr='--standardFiber %s', extensions=None), testFiber=dict(argstr='--testFiber %s', extensions=None), testForBijection=dict(argstr='--testForBijection '), testForFiberCardinality=dict(argstr='--testForFiberCardinality '), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), closeness=dict(argstr='--closeness %f'), environ=dict(nohash=True, usedefault=True), numberOfPoints=dict(argstr='--numberOfPoints %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), standardFiber=dict(argstr='--standardFiber %s', extensions=None), testFiber=dict(argstr='--testFiber %s', extensions=None), testForBijection=dict(argstr='--testForBijection '), testForFiberCardinality=dict(argstr='--testForFiberCardinality '), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```

## Next Steps


---

*Source: test_auto_compareTractInclusion.py:6 | Complexity: Beginner | Last updated: 2026-05-18*