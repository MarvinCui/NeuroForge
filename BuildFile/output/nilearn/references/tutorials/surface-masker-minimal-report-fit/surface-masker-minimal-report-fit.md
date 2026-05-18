# How To: Surface Masker Minimal Report Fit

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test minimal report generation with fit.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `collections`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn._utils.helpers`
- `nilearn._utils.tags`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.reporting`
- `nilearn.reporting.tests._testing`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: surf_mask_1d, empty_mask, surf_img_1d, reports
```

## Step-by-Step Guide

### Step 1: 'Test minimal report generation with fit.'

```python
'Test minimal report generation with fit.'
```

**Verification:**
```python
assert float(masker._report_content['coverage']) > 0
```

### Step 2: Assign mask = value

```python
mask = None if empty_mask else surf_mask_1d
```

### Step 3: Assign masker = SurfaceMasker(...)

```python
masker = SurfaceMasker(mask_img=mask, reports=reports, standardize=None)
```

### Step 4: Call masker.fit_transform()

```python
masker.fit_transform(surf_img_1d)
```

### Step 5: Assign extend_includes = value

```python
extend_includes = []
```

### Step 6: Call generate_and_check_masker_report()

```python
generate_and_check_masker_report(masker, extend_includes=extend_includes)
```

### Step 7: Assign extend_includes = value

```python
extend_includes = ['The mask includes']
```

**Verification:**
```python
assert float(masker._report_content['coverage']) > 0
```


## Complete Example

```python
# Setup
# Fixtures: surf_mask_1d, empty_mask, surf_img_1d, reports

# Workflow
'Test minimal report generation with fit.'
mask = None if empty_mask else surf_mask_1d
masker = SurfaceMasker(mask_img=mask, reports=reports, standardize=None)
masker.fit_transform(surf_img_1d)
extend_includes = []
if reports:
    extend_includes = ['The mask includes']
generate_and_check_masker_report(masker, extend_includes=extend_includes)
if reports:
    assert float(masker._report_content['coverage']) > 0
```

## Next Steps


---

*Source: test_html_report.py:571 | Complexity: Intermediate | Last updated: 2026-05-18*