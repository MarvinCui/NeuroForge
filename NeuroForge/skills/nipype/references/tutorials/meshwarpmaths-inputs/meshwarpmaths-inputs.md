# How To: Meshwarpmaths Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MeshWarpMaths inputs

## Prerequisites

**Required Modules:**
- `mesh`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(float_trait=dict(), in_surf=dict(extensions=None, mandatory=True), operation=dict(usedefault=True), operator=dict(mandatory=True, usedefault=True), out_file=dict(extensions=None, usedefault=True), out_warp=dict(extensions=None, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(float_trait=dict(), in_surf=dict(extensions=None, mandatory=True), operation=dict(usedefault=True), operator=dict(mandatory=True, usedefault=True), out_file=dict(extensions=None, usedefault=True), out_warp=dict(extensions=None, usedefault=True))
```

## Next Steps


---

*Source: test_auto_MeshWarpMaths.py:6 | Complexity: Beginner | Last updated: 2026-05-18*