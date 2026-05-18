# How To: Masker Reporting True

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test nilearn.maskers._mixin._ReportingMixin on concrete masker
instances when ``reports=True``.

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
# Fixtures: masker, img_func, kwargs
```

## Step-by-Step Guide

### Step 1: 'Test nilearn.maskers._mixin._ReportingMixin on concrete masker\n    instances when ``reports=True``.\n    '

```python
'Test nilearn.maskers._mixin._ReportingMixin on concrete masker\n    instances when ``reports=True``.\n    '
```

**Verification:**
```python
assert masker._report_warnings == []
```

### Step 2: Assign masker = clone(...)

```python
masker = clone(masker)
```

**Verification:**
```python
assert masker._has_report_data() is False
```

### Step 3: Call generate_and_check_masker_report()

```python
generate_and_check_masker_report(masker, **kwargs)
```

**Verification:**
```python
assert masker._has_report_data()
```

### Step 4: Assign input_img = img_func(...)

```python
input_img = img_func()
```

**Verification:**
```python
assert match in str(report)
```

### Step 5: Call masker.fit()

```python
masker.fit(input_img)
```

**Verification:**
```python
assert masker._has_report_data()
```

### Step 6: Assign extra_warnings_allowed = False

```python
extra_warnings_allowed = False
```

### Step 7: Call generate_and_check_masker_report()

```python
generate_and_check_masker_report(masker, extra_warnings_allowed=extra_warnings_allowed, **kwargs)
```

### Step 8: Call generate_and_check_masker_report()

```python
generate_and_check_masker_report(masker, title='masker report title', extra_warnings_allowed=extra_warnings_allowed, **kwargs)
```

### Step 9: Assign masker.reports = False

```python
masker.reports = False
```

### Step 10: Assign match = 'Report generation not enabled'

```python
match = 'Report generation not enabled'
```

**Verification:**
```python
assert match in str(report)
```

### Step 11: Assign extra_warnings_allowed = True

```python
extra_warnings_allowed = True
```

### Step 12: Assign report = masker.generate_report(...)

```python
report = masker.generate_report(**kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: masker, img_func, kwargs

# Workflow
'Test nilearn.maskers._mixin._ReportingMixin on concrete masker\n    instances when ``reports=True``.\n    '
masker = clone(masker)
assert masker._report_warnings == []
generate_and_check_masker_report(masker, **kwargs)
assert masker._has_report_data() is False
input_img = img_func()
masker.fit(input_img)
assert masker._has_report_data()
extra_warnings_allowed = False
if isinstance(masker, SurfaceMapsMasker):
    extra_warnings_allowed = True
generate_and_check_masker_report(masker, extra_warnings_allowed=extra_warnings_allowed, **kwargs)
generate_and_check_masker_report(masker, title='masker report title', extra_warnings_allowed=extra_warnings_allowed, **kwargs)
masker.reports = False
match = 'Report generation not enabled'
with pytest.warns(UserWarning, match=match):
    report = masker.generate_report(**kwargs)
assert match in str(report)
```

## Next Steps


---

*Source: test_mixin.py:92 | Complexity: Advanced | Last updated: 2026-05-18*