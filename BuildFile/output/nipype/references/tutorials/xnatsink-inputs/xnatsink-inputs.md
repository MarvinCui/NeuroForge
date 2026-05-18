# How To: Xnatsink Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test XNATSink inputs

## Prerequisites

**Required Modules:**
- `io`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(_outputs=dict(usedefault=True), assessor_id=dict(xor=['reconstruction_id']), cache_dir=dict(), config=dict(extensions=None, mandatory=True, xor=['server']), experiment_id=dict(mandatory=True), project_id=dict(mandatory=True), pwd=dict(), reconstruction_id=dict(xor=['assessor_id']), server=dict(mandatory=True, requires=['user', 'pwd'], xor=['config']), share=dict(usedefault=True), subject_id=dict(mandatory=True), user=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(_outputs=dict(usedefault=True), assessor_id=dict(xor=['reconstruction_id']), cache_dir=dict(), config=dict(extensions=None, mandatory=True, xor=['server']), experiment_id=dict(mandatory=True), project_id=dict(mandatory=True), pwd=dict(), reconstruction_id=dict(xor=['assessor_id']), server=dict(mandatory=True, requires=['user', 'pwd'], xor=['config']), share=dict(usedefault=True), subject_id=dict(mandatory=True), user=dict())
```

## Next Steps


---

*Source: test_auto_XNATSink.py:6 | Complexity: Beginner | Last updated: 2026-05-18*