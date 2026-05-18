# How To: Displayed Maps Valid Inputs

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test valid inputs for displayed_maps/spheres.

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
# Fixtures: masker_class, input_parameters, displayed_maps, expected_displayed_maps
```

## Step-by-Step Guide

### Step 1: 'Test valid inputs for displayed_maps/spheres.'

```python
'Test valid inputs for displayed_maps/spheres.'
```

**Verification:**
```python
assert masker._report_content['displayed_maps'] == expected_displayed_maps
```

### Step 2: Assign masker = masker_class(...)

```python
masker = masker_class(**input_parameters)
```

**Verification:**
```python
assert html.body.count('<img') == len(expected_displayed_maps)
```

### Step 3: Call masker.fit()

```python
masker.fit()
```

**Verification:**
```python
assert masker._report_content['displayed_maps'] == expected_displayed_maps
```

### Step 4: Assign html = masker.generate_report(...)

```python
html = masker.generate_report(displayed_spheres=displayed_maps)
```

### Step 5: Assign html = masker.generate_report(...)

```python
html = masker.generate_report(displayed_maps=displayed_maps)
```

### Step 6: Assign tmp = value

```python
tmp = [0, *[x + 1 for x in expected_displayed_maps]]
```

### Step 7: Assign expected_displayed_maps = tmp

```python
expected_displayed_maps = tmp
```


## Complete Example

```python
# Setup
# Fixtures: masker_class, input_parameters, displayed_maps, expected_displayed_maps

# Workflow
'Test valid inputs for displayed_maps/spheres.'
masker = masker_class(**input_parameters)
masker.fit()
if isinstance(masker, NiftiSpheresMasker):
    html = masker.generate_report(displayed_spheres=displayed_maps)
else:
    html = masker.generate_report(displayed_maps=displayed_maps)
if isinstance(masker, NiftiSpheresMasker):
    tmp = [0, *[x + 1 for x in expected_displayed_maps]]
    expected_displayed_maps = tmp
assert masker._report_content['displayed_maps'] == expected_displayed_maps
assert html.body.count('<img') == len(expected_displayed_maps)
```

## Next Steps


---

*Source: test_html_report.py:177 | Complexity: Intermediate | Last updated: 2026-05-18*