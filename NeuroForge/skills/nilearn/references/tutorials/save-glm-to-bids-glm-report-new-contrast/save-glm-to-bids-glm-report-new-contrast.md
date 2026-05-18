# How To: Save Glm To Bids Glm Report New Contrast

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Run generate_report after save_glm_to_bids with different contrasts.

generate_report tries to rely on some of the generated output,
but if different contrasts are requested
then it will have to do some extra contrast computation.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `warnings`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.glm.first_level`
- `nilearn.glm.io`
- `nilearn.glm.second_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: two_runs_model, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Run generate_report after save_glm_to_bids with different contrasts.\n\n    generate_report tries to rely on some of the generated output,\n    but if different contrasts are requested\n    then it will have to do some extra contrast computation.\n    '

```python
'Run generate_report after save_glm_to_bids with different contrasts.\n\n    generate_report tries to rely on some of the generated output,\n    but if different contrasts are requested\n    then it will have to do some extra contrast computation.\n    '
```

**Verification:**
```python
assert 'AAA-BBB' in report.__str__()
```

### Step 2: Assign contrasts = value

```python
contrasts = {'BBB-AAA': 'BBB-AAA'}
```

**Verification:**
```python
assert 'BBB-AAA' not in report.__str__()
```

### Step 3: Assign contrast_types = value

```python
contrast_types = {'BBB-AAA': 't'}
```

**Verification:**
```python
assert file not in report.__str__()
```

### Step 4: Assign model = save_glm_to_bids(...)

```python
model = save_glm_to_bids(model=two_runs_model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmp_path, **KWARGS)
```

### Step 5: Assign EXPECTED_FILENAMES = value

```python
EXPECTED_FILENAMES = ['run-1_design.png', 'run-1_corrdesign.png', 'run-1_contrast-bbbMinusAaa_design.png']
```

### Step 6: Assign report = model.generate_report(...)

```python
report = model.generate_report(contrasts=['AAA-BBB'], **KWARGS)
```

**Verification:**
```python
assert 'AAA-BBB' in report.__str__()
```


## Complete Example

```python
# Setup
# Fixtures: two_runs_model, tmp_path

# Workflow
'Run generate_report after save_glm_to_bids with different contrasts.\n\n    generate_report tries to rely on some of the generated output,\n    but if different contrasts are requested\n    then it will have to do some extra contrast computation.\n    '
contrasts = {'BBB-AAA': 'BBB-AAA'}
contrast_types = {'BBB-AAA': 't'}
model = save_glm_to_bids(model=two_runs_model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmp_path, **KWARGS)
EXPECTED_FILENAMES = ['run-1_design.png', 'run-1_corrdesign.png', 'run-1_contrast-bbbMinusAaa_design.png']
report = model.generate_report(contrasts=['AAA-BBB'], **KWARGS)
assert 'AAA-BBB' in report.__str__()
assert 'BBB-AAA' not in report.__str__()
for file in EXPECTED_FILENAMES:
    assert file not in report.__str__()
```

## Next Steps


---

*Source: test_io.py:448 | Complexity: Intermediate | Last updated: 2026-05-18*