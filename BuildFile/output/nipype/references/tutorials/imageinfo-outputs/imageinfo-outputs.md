# How To: Imageinfo Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ImageInfo outputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(TE=dict(), TI=dict(), TR=dict(), data_type=dict(), dimensions=dict(), file_format=dict(), info=dict(), orientation=dict(), out_file=dict(extensions=None), ph_enc_dir=dict(), vox_sizes=dict())
```


## Complete Example

```python
# Workflow
output_map = dict(TE=dict(), TI=dict(), TR=dict(), data_type=dict(), dimensions=dict(), file_format=dict(), info=dict(), orientation=dict(), out_file=dict(extensions=None), ph_enc_dir=dict(), vox_sizes=dict())
```

## Next Steps


---

*Source: test_auto_ImageInfo.py:29 | Complexity: Beginner | Last updated: 2026-05-18*