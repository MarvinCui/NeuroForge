# How To: Multiplyimages Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MultiplyImages inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), first_input=dict(argstr='%s', extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), output_product_image=dict(argstr='%s', extensions=None, mandatory=True, position=3), second_input=dict(argstr='%s', mandatory=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), first_input=dict(argstr='%s', extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), output_product_image=dict(argstr='%s', extensions=None, mandatory=True, position=3), second_input=dict(argstr='%s', mandatory=True, position=2))
```

## Next Steps


---

*Source: test_auto_MultiplyImages.py:6 | Complexity: Beginner | Last updated: 2026-05-18*