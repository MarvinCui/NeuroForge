# How To: Pr Links Are Formatted

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: mock

## Overview

Configuration example: Test that PR links are formatted correctly in the release body.

## Prerequisites

**Required Modules:**
- `re`
- `publish_release_notes_to_discourse`


## Step-by-Step Guide

### Step 1: Assign config = value

```python
config = {'RELEASE_TAG': 'v5.26.0', 'REPO_NAME': 'pymc-devs/pymc', 'RELEASE_BODY': release_body, 'RELEASE_URL': 'https://github.com/pymc-devs/pymc/releases/tag/v5.26.0'}
```


## Complete Example

```python
# Workflow
config = {'RELEASE_TAG': 'v5.26.0', 'REPO_NAME': 'pymc-devs/pymc', 'RELEASE_BODY': release_body, 'RELEASE_URL': 'https://github.com/pymc-devs/pymc/releases/tag/v5.26.0'}
```

## Next Steps


---

*Source: test_publish_release_notes.py:50 | Complexity: Beginner | Last updated: 2026-05-18*