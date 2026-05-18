# How To: Gtractresampledwiinplace Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractResampleDWIInPlace inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), debugLevel=dict(argstr='--debugLevel %d'), environ=dict(nohash=True, usedefault=True), imageOutputSize=dict(argstr='--imageOutputSize %s', sep=','), inputTransform=dict(argstr='--inputTransform %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputResampledB0=dict(argstr='--outputResampledB0 %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None), warpDWITransform=dict(argstr='--warpDWITransform %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), debugLevel=dict(argstr='--debugLevel %d'), environ=dict(nohash=True, usedefault=True), imageOutputSize=dict(argstr='--imageOutputSize %s', sep=','), inputTransform=dict(argstr='--inputTransform %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputResampledB0=dict(argstr='--outputResampledB0 %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None), warpDWITransform=dict(argstr='--warpDWITransform %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_gtractResampleDWIInPlace.py:6 | Complexity: Beginner | Last updated: 2026-05-18*