# How To: Datasink Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DataSink inputs

## Prerequisites

**Required Modules:**
- `io`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(_outputs=dict(usedefault=True), base_directory=dict(), bucket=dict(), container=dict(), creds_path=dict(), encrypt_bucket_keys=dict(), local_copy=dict(), parameterization=dict(usedefault=True), regexp_substitutions=dict(), remove_dest_dir=dict(usedefault=True), strip_dir=dict(), substitutions=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(_outputs=dict(usedefault=True), base_directory=dict(), bucket=dict(), container=dict(), creds_path=dict(), encrypt_bucket_keys=dict(), local_copy=dict(), parameterization=dict(usedefault=True), regexp_substitutions=dict(), remove_dest_dir=dict(usedefault=True), strip_dir=dict(), substitutions=dict())
```

## Next Steps


---

*Source: test_auto_DataSink.py:6 | Complexity: Beginner | Last updated: 2026-05-18*