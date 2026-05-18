# How To: Masker

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Configuration example: Fixture to construct a masker instance with proper input.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `sklearn`
- `nilearn._utils.helpers`
- `nilearn.conftest`
- `nilearn.maskers`
- `nilearn.maskers.tests.test_html_report`

**Setup Required:**
```python
# Fixtures: request, img_maps, surf_maps_img, img_labels, surf_label_img
```

## Step-by-Step Guide

### Step 1: Assign img_generators = value

```python
img_generators = {'img_maps': img_maps, 'surf_maps_img': surf_maps_img, 'img_labels': img_labels, 'surf_label_img': surf_label_img}
```


## Complete Example

```python
# Setup
# Fixtures: request, img_maps, surf_maps_img, img_labels, surf_label_img

# Workflow
img_generators = {'img_maps': img_maps, 'surf_maps_img': surf_maps_img, 'img_labels': img_labels, 'surf_label_img': surf_label_img}
```

## Next Steps


---

*Source: test_mixin.py:31 | Complexity: Beginner | Last updated: 2026-05-18*