# How To: Flameo Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FLAMEO outputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(copes=dict(), fstats=dict(), mrefvars=dict(), pes=dict(), res4d=dict(), stats_dir=dict(), tdof=dict(), tstats=dict(), var_copes=dict(), weights=dict(), zfstats=dict(), zstats=dict())
```


## Complete Example

```python
# Workflow
output_map = dict(copes=dict(), fstats=dict(), mrefvars=dict(), pes=dict(), res4d=dict(), stats_dir=dict(), tdof=dict(), tstats=dict(), var_copes=dict(), weights=dict(), zfstats=dict(), zstats=dict())
```

## Next Steps


---

*Source: test_auto_FLAMEO.py:93 | Complexity: Beginner | Last updated: 2026-05-18*