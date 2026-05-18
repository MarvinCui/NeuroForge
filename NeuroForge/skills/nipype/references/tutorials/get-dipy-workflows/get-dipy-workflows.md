# How To: Get Dipy Workflows

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test get dipy workflows

## Prerequisites

**Required Modules:**
- `pytest`
- `packaging.version`
- `collections`
- `base`
- `base`
- `dipy.utils.deprecator`
- `dipy.workflows.workflow`
- `dipy.workflows`


## Step-by-Step Guide

### Step 1: Assign l_wkflw = get_dipy_workflows(...)

```python
l_wkflw = get_dipy_workflows(align)
```

**Verification:**
```python
assert name.endswith('Flow')
```


## Complete Example

```python
# Workflow
from dipy.workflows import align
l_wkflw = get_dipy_workflows(align)
for name, obj in l_wkflw:
    assert name.endswith('Flow')
    assert issubclass(obj, align.Workflow)
```

## Next Steps


---

*Source: test_base.py:200 | Complexity: Beginner | Last updated: 2026-05-18*