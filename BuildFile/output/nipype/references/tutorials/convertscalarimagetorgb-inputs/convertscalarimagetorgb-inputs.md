# How To: Convertscalarimagetorgb Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ConvertScalarImageToRGB inputs

## Prerequisites

**Required Modules:**
- `visualization`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), colormap=dict(argstr='%s', mandatory=True, position=4), custom_color_map_file=dict(argstr='%s', position=5, usedefault=True), dimension=dict(argstr='%d', mandatory=True, position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=1), mask_image=dict(argstr='%s', position=3, usedefault=True), maximum_RGB_output=dict(argstr='%d', position=9, usedefault=True), maximum_input=dict(argstr='%d', mandatory=True, position=7), minimum_RGB_output=dict(argstr='%d', position=8, usedefault=True), minimum_input=dict(argstr='%d', mandatory=True, position=6), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='%s', position=2, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), colormap=dict(argstr='%s', mandatory=True, position=4), custom_color_map_file=dict(argstr='%s', position=5, usedefault=True), dimension=dict(argstr='%d', mandatory=True, position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=1), mask_image=dict(argstr='%s', position=3, usedefault=True), maximum_RGB_output=dict(argstr='%d', position=9, usedefault=True), maximum_input=dict(argstr='%d', mandatory=True, position=7), minimum_RGB_output=dict(argstr='%d', position=8, usedefault=True), minimum_input=dict(argstr='%d', mandatory=True, position=6), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='%s', position=2, usedefault=True))
```

## Next Steps


---

*Source: test_auto_ConvertScalarImageToRGB.py:6 | Complexity: Beginner | Last updated: 2026-05-18*