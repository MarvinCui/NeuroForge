# How To: Xnatsource Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test XNATSource inputs

## Prerequisites

**Required Modules:**
- `io`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(cache_dir=dict(), config=dict(extensions=None, mandatory=True, xor=['server']), pwd=dict(), query_template=dict(mandatory=True), query_template_args=dict(usedefault=True), server=dict(mandatory=True, requires=['user', 'pwd'], xor=['config']), user=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(cache_dir=dict(), config=dict(extensions=None, mandatory=True, xor=['server']), pwd=dict(), query_template=dict(mandatory=True), query_template_args=dict(usedefault=True), server=dict(mandatory=True, requires=['user', 'pwd'], xor=['config']), user=dict())
```

## Next Steps


---

*Source: test_auto_XNATSource.py:6 | Complexity: Beginner | Last updated: 2026-05-18*