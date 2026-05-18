# How To: Write Report

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test write report

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `pytest`
- `bidsschematools.conftest`
- `bidsschematools.validator`
- `data`
- `data`
- `bidsschematools.validator`
- `bidsschematools.validator`
- `bidsschematools.validator`
- `bidsschematools`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign validation_result = value

```python
validation_result = {}
```

**Verification:**
```python
assert report_path.read_text() == expected_report_path.read_text()
```

### Step 2: Assign unknown = value

```python
validation_result['schema_tracking'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9a-zA-Z+]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
```

### Step 3: Assign unknown = value

```python
validation_result['schema_listing'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
```

### Step 4: Assign unknown = value

```python
validation_result['path_tracking'] = ['/home/chymera/.data2/datalad/000026/noncompliant/sub-EXC022/anat/sub-EXC022_ses-MRI_flip-1_VFA.nii.gz']
```

### Step 5: Assign unknown = value

```python
validation_result['path_listing'] = ['/home/chymera/.data2/datalad/000026/noncompliant/sub-EXC022/anat/sub-EXC022_ses-MRI_flip-1_VFA.nii.gz']
```

### Step 6: Assign report_path = value

```python
report_path = tmp_path / 'output_bids_validator_xs_write.log'
```

### Step 7: Call write_report()

```python
write_report(validation_result, report_path=str(report_path))
```

### Step 8: Assign expected_report_path = load_test_data(...)

```python
expected_report_path = load_test_data('expected_bids_validator_xs_write.log')
```

**Verification:**
```python
assert report_path.read_text() == expected_report_path.read_text()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
from bidsschematools.validator import write_report
validation_result = {}
validation_result['schema_tracking'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9a-zA-Z+]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
validation_result['schema_listing'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
validation_result['path_tracking'] = ['/home/chymera/.data2/datalad/000026/noncompliant/sub-EXC022/anat/sub-EXC022_ses-MRI_flip-1_VFA.nii.gz']
validation_result['path_listing'] = ['/home/chymera/.data2/datalad/000026/noncompliant/sub-EXC022/anat/sub-EXC022_ses-MRI_flip-1_VFA.nii.gz']
report_path = tmp_path / 'output_bids_validator_xs_write.log'
write_report(validation_result, report_path=str(report_path))
expected_report_path = load_test_data('expected_bids_validator_xs_write.log')
assert report_path.read_text() == expected_report_path.read_text()
```

## Next Steps


---

*Source: test_validator.py:68 | Complexity: Advanced | Last updated: 2026-05-18*