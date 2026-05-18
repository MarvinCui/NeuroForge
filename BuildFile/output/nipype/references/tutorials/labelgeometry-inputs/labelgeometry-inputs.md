# How To: Labelgeometry Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test LabelGeometry inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), intensity_image=dict(argstr='%s', extensions=None, mandatory=True, position=2, usedefault=True), label_image=dict(argstr='%s', extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), output_file=dict(argstr='%s', name_source=['label_image'], name_template='%s.csv', position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), intensity_image=dict(argstr='%s', extensions=None, mandatory=True, position=2, usedefault=True), label_image=dict(argstr='%s', extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), output_file=dict(argstr='%s', name_source=['label_image'], name_template='%s.csv', position=3))
```

## Next Steps


---

*Source: test_auto_LabelGeometry.py:6 | Complexity: Beginner | Last updated: 2026-05-18*