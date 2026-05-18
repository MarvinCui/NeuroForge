# How To: Measureimagesimilarity Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MeasureImageSimilarity inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='--dimensionality %d', position=1), environ=dict(nohash=True, usedefault=True), fixed_image=dict(extensions=None, mandatory=True), fixed_image_mask=dict(argstr='%s', extensions=None), metric=dict(argstr='%s', mandatory=True), metric_weight=dict(requires=['metric'], usedefault=True), moving_image=dict(extensions=None, mandatory=True), moving_image_mask=dict(extensions=None, requires=['fixed_image_mask']), num_threads=dict(nohash=True, usedefault=True), radius_or_number_of_bins=dict(mandatory=True, requires=['metric']), sampling_percentage=dict(mandatory=True, requires=['metric']), sampling_strategy=dict(requires=['metric'], usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='--dimensionality %d', position=1), environ=dict(nohash=True, usedefault=True), fixed_image=dict(extensions=None, mandatory=True), fixed_image_mask=dict(argstr='%s', extensions=None), metric=dict(argstr='%s', mandatory=True), metric_weight=dict(requires=['metric'], usedefault=True), moving_image=dict(extensions=None, mandatory=True), moving_image_mask=dict(extensions=None, requires=['fixed_image_mask']), num_threads=dict(nohash=True, usedefault=True), radius_or_number_of_bins=dict(mandatory=True, requires=['metric']), sampling_percentage=dict(mandatory=True, requires=['metric']), sampling_strategy=dict(requires=['metric'], usedefault=True))
```

## Next Steps


---

*Source: test_auto_MeasureImageSimilarity.py:6 | Complexity: Beginner | Last updated: 2026-05-18*