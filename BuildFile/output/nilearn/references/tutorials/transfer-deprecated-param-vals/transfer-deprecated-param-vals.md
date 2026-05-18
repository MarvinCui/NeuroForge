# How To: Transfer Deprecated Param Vals

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: mock

## Overview

Configuration example: Check that values assigned to deprecated parameters are        correctly reassigned to the replacement parameters.
    

## Prerequisites

**Required Modules:**
- `warnings`
- `pathlib`
- `unittest.mock`
- `pytest`
- `nilearn._utils.helpers`


## Step-by-Step Guide

### Step 1: Assign expected_output = value

```python
expected_output = {'unchanged_param_0': 'unchanged_param_0_val', 'replacement_param_0': 'deprecated_param_0_val', 'replacement_param_1': 'deprecated_param_1_val', 'unchanged_param_1': 'unchanged_param_1_val'}
```


## Complete Example

```python
# Workflow
expected_output = {'unchanged_param_0': 'unchanged_param_0_val', 'replacement_param_0': 'deprecated_param_0_val', 'replacement_param_1': 'deprecated_param_1_val', 'unchanged_param_1': 'unchanged_param_1_val'}
```

## Next Steps


---

*Source: test_helpers.py:179 | Complexity: Beginner | Last updated: 2026-05-18*