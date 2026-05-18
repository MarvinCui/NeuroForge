# How To: Release Structure

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Configuration example: Test that the overall release structure is correct.

## Prerequisites

**Required Modules:**
- `re`
- `publish_release_notes_to_discourse`


## Step-by-Step Guide

### Step 1: Assign config = value

```python
config = {'RELEASE_TAG': 'v1.2.3', 'REPO_NAME': 'pymc-devs/pymc', 'RELEASE_BODY': 'Test body with PR https://github.com/pymc-devs/pymc/pull/999', 'RELEASE_URL': 'https://github.com/pymc-devs/pymc/releases/tag/v1.2.3'}
```


## Complete Example

```python
# Workflow
config = {'RELEASE_TAG': 'v1.2.3', 'REPO_NAME': 'pymc-devs/pymc', 'RELEASE_BODY': 'Test body with PR https://github.com/pymc-devs/pymc/pull/999', 'RELEASE_URL': 'https://github.com/pymc-devs/pymc/releases/tag/v1.2.3'}
```

## Next Steps


---

*Source: test_publish_release_notes.py:117 | Complexity: Beginner | Last updated: 2026-05-18*