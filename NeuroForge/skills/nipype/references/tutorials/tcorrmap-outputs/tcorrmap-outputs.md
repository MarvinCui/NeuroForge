# How To: Tcorrmap Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TCorrMap outputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(absolute_threshold=dict(extensions=None), average_expr=dict(extensions=None), average_expr_nonzero=dict(extensions=None), correlation_maps=dict(extensions=None), correlation_maps_masked=dict(extensions=None), histogram=dict(extensions=None), mean_file=dict(extensions=None), pmean=dict(extensions=None), qmean=dict(extensions=None), sum_expr=dict(extensions=None), var_absolute_threshold=dict(extensions=None), var_absolute_threshold_normalize=dict(extensions=None), zmean=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(absolute_threshold=dict(extensions=None), average_expr=dict(extensions=None), average_expr_nonzero=dict(extensions=None), correlation_maps=dict(extensions=None), correlation_maps_masked=dict(extensions=None), histogram=dict(extensions=None), mean_file=dict(extensions=None), pmean=dict(extensions=None), qmean=dict(extensions=None), sum_expr=dict(extensions=None), var_absolute_threshold=dict(extensions=None), var_absolute_threshold_normalize=dict(extensions=None), zmean=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_TCorrMap.py:166 | Complexity: Beginner | Last updated: 2026-05-18*