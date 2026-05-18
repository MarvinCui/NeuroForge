# How To: Expand

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Configuration example: test expand

## Prerequisites

**Required Modules:**
- `pathlib`
- `snakemake.io`
- `snakemake.exceptions`


## Step-by-Step Guide

### Step 1: Assign wildcards = value

```python
wildcards = {'a': [1, 2], 'b': [3, 4], 'c': [5]}
```


## Complete Example

```python
# Workflow
wildcards = {'a': [1, 2], 'b': [3, 4], 'c': [5]}
```

## Next Steps


---

*Source: test_io.py:44 | Complexity: Beginner | Last updated: 2026-05-18*