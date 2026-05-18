# How To: Histogrammatchingfilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test HistogramMatchingFilter inputs

## Prerequisites

**Required Modules:**
- `utilities`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), histogramAlgorithm=dict(argstr='--histogramAlgorithm %s'), inputBinaryVolume=dict(argstr='--inputBinaryVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), numberOfMatchPoints=dict(argstr='--numberOfMatchPoints %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), referenceBinaryVolume=dict(argstr='--referenceBinaryVolume %s', extensions=None), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None), verbose=dict(argstr='--verbose '), writeHistogram=dict(argstr='--writeHistogram %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), histogramAlgorithm=dict(argstr='--histogramAlgorithm %s'), inputBinaryVolume=dict(argstr='--inputBinaryVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), numberOfMatchPoints=dict(argstr='--numberOfMatchPoints %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), referenceBinaryVolume=dict(argstr='--referenceBinaryVolume %s', extensions=None), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None), verbose=dict(argstr='--verbose '), writeHistogram=dict(argstr='--writeHistogram %s'))
```

## Next Steps


---

*Source: test_auto_HistogramMatchingFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*