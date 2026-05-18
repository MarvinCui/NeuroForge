# How To: Denoise Inputs

**Difficulty**: Intermediate
**Estimated Time**: 5 minutes
**Tags**: mock

## Overview

Instantiate dict: test Denoise inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(block_radius=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None), noise_mask=dict(extensions=None), noise_model=dict(mandatory=True, usedefault=True), patch_radius=dict(usedefault=True), signal_mask=dict(extensions=None), snr=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(block_radius=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None), noise_mask=dict(extensions=None), noise_model=dict(mandatory=True, usedefault=True), patch_radius=dict(usedefault=True), signal_mask=dict(extensions=None), snr=dict())
```

## Next Steps


---

*Source: test_auto_Denoise.py:6 | Complexity: Intermediate | Last updated: 2026-05-18*