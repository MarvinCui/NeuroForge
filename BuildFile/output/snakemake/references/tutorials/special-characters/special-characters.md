# How To: Special Characters

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate PrefixLookup: test special characters

## Prerequisites

**Required Modules:**
- `snakemake.common.prefix_lookup`


## Step-by-Step Guide

### Step 1: Assign lookup = PrefixLookup(...)

```python
lookup = PrefixLookup([(' ', 1), ('\t', 2), ('\n', 3), ('$#@!', 4), ('test$', 5)])
```


## Complete Example

```python
# Workflow
lookup = PrefixLookup([(' ', 1), ('\t', 2), ('\n', 3), ('$#@!', 4), ('test$', 5)])
```

## Next Steps


---

*Source: test_prefix_lookup.py:50 | Complexity: Beginner | Last updated: 2026-05-18*