# How To: Bedpostx5 Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BEDPOSTX5 outputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(dyads=dict(), dyads_dispersion=dict(), mean_S0samples=dict(extensions=None), mean_dsamples=dict(extensions=None), mean_fsamples=dict(), mean_phsamples=dict(), mean_thsamples=dict(), merged_fsamples=dict(), merged_phsamples=dict(), merged_thsamples=dict())
```


## Complete Example

```python
# Workflow
output_map = dict(dyads=dict(), dyads_dispersion=dict(), mean_S0samples=dict(extensions=None), mean_dsamples=dict(extensions=None), mean_fsamples=dict(), mean_phsamples=dict(), mean_thsamples=dict(), merged_fsamples=dict(), merged_phsamples=dict(), merged_thsamples=dict())
```

## Next Steps


---

*Source: test_auto_BEDPOSTX5.py:125 | Complexity: Beginner | Last updated: 2026-05-18*