# How To: Non Pymc Links Unchanged

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Configuration example: Test that PR links from other repositories are not affected.

## Prerequisites

**Required Modules:**
- `re`
- `publish_release_notes_to_discourse`


## Step-by-Step Guide

### Step 1: Assign config = value

```python
config = {'RELEASE_TAG': 'v1.0.0', 'REPO_NAME': 'pymc-devs/pymc', 'RELEASE_BODY': release_body, 'RELEASE_URL': 'https://github.com/pymc-devs/pymc/releases/tag/v1.0.0'}
```


## Complete Example

```python
# Workflow
config = {'RELEASE_TAG': 'v1.0.0', 'REPO_NAME': 'pymc-devs/pymc', 'RELEASE_BODY': release_body, 'RELEASE_URL': 'https://github.com/pymc-devs/pymc/releases/tag/v1.0.0'}
```

## Next Steps


---

*Source: test_publish_release_notes.py:99 | Complexity: Beginner | Last updated: 2026-05-18*