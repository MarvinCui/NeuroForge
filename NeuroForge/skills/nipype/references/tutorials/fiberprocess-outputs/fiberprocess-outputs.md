# How To: Fiberprocess Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fiberprocess outputs

## Prerequisites

**Required Modules:**
- `fiberprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(fiber_output=dict(extensions=None), voxelize=dict(extensions=None))
```

**Verification:**
```python
assert getattr(outputs.traits()[key], metakey) == value
```

### Step 2: Assign outputs = fiberprocess.output_spec(...)

```python
outputs = fiberprocess.output_spec()
```

**Verification:**
```python
assert getattr(outputs.traits()[key], metakey) == value
```


## Complete Example

```python
# Workflow
output_map = dict(fiber_output=dict(extensions=None), voxelize=dict(extensions=None))
outputs = fiberprocess.output_spec()
for key, metadata in list(output_map.items()):
    for metakey, value in list(metadata.items()):
        assert getattr(outputs.traits()[key], metakey) == value
```

## Next Steps


---

*Source: test_auto_fiberprocess.py:70 | Complexity: Beginner | Last updated: 2026-05-18*