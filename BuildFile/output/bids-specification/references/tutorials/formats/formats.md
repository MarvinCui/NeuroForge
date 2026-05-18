# How To: Formats

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test valid string patterns allowed by the specification.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `os`
- `subprocess`
- `collections.abc`
- `pytest`
- `jsonschema.exceptions`
- `bidsschematools`
- `data`
- `re`

**Setup Required:**
```python
# Fixtures: schema_obj
```

## Step-by-Step Guide

### Step 1: 'Test valid string patterns allowed by the specification.'

```python
'Test valid string patterns allowed by the specification.'
```

**Verification:**
```python
assert bool(search.fullmatch(test_string)), f"'{test_string}' is not a valid match for the pattern '{search.pattern}'"
```

### Step 2: Assign GOOD_PATTERNS = value

```python
GOOD_PATTERNS = {'label': ['01', 'test', 'test01', 'Test01'], 'index': ['01', '1', '10000', '00001'], 'string': ['any string is valid.'], 'integer': ['5', '10', '-5', '-10'], 'number': ['5', '3.14', '-5', '-3.14', '1e3', '-2.1E+5'], 'boolean': ['true', 'false'], 'date': ['2022-01-05', '2022-01-05UTC', '2022-50-50'], 'datetime': ['2022-01-05T13:16:30', '2022-01-05T13:16:30.5', '2022-01-05T13:16:30.000005', '2022-01-05T13:16:30Z', '2022-01-05T13:16:30.05Z', '2022-01-05T13:16:30+01:00', '2022-01-05T13:16:30-05:00'], 'time': ['13:16:30', '09:00:00', '9:00:00'], 'unit': ['any string is valid.'], 'file_relative': ['file_in_same_directory.txt', '../../relative/path/file.txt', 'sub-01/path/file.txt'], 'stimuli_relative': ['any/arbitrary/path/file.txt'], 'dataset_relative': ['any/arbitrary/path/file.txt'], 'participant_relative': ['any/arbitrary/path/file.txt'], 'rrid': ['RRID:SCR_017398'], 'uri': ['foo://example.com:8042/over/there?name=ferret#nose'], 'bids_uri': ['bids::sub-01/fmap/sub-01_dir-AP_epi.nii.gz', 'bids:ds000001:sub-02/anat/sub-02_T1w.nii.gz', 'bids:myderivatives:sub-03/func/sub-03_task-rest_space-MNI152_bold.nii.gz']}
```

**Verification:**
```python
assert not bool(search.fullmatch(test_string)), f"'{test_string}' should not be a valid match for the pattern '{search.pattern}'"
```

### Step 3: Assign BAD_PATTERNS = value

```python
BAD_PATTERNS = {'label': ['test_01', '!', '010101-', '01-01', '-01'], 'index': ['test', '0.1', '0-1', '0_1'], 'string': [], 'integer': ['3.14', '-3.14', '1.', '-1.', 'string', 's1', '1%', 'one'], 'number': ['string', '1%'], 'boolean': ['True', 'False', 'T', 'F'], 'date': ['05-01-2022', '05/01/2022'], 'datetime': ['2022-01-05T13:16:30.1000005', '2022-01-05T13:16:30U', '2022-01-05T13:16:30UTCUTC', '2022-01-05T34:10:10'], 'time': ['34:10:10', '24:00:00', '00:60:00', '00:00:60', '01:23'], 'unit': [], 'file_relative': ['/path/with/starting/slash/file.txt'], 'stimuli_relative': ['/path/with/starting/slash/file.txt', 'stimuli/path/file.txt'], 'dataset_relative': ['/path/with/starting/slash/file.txt'], 'participant_relative': ['/path/with/starting/slash/file.txt', 'sub-01/path/file.txt'], 'rrid': ['RRID:'], 'uri': [], 'bids_uri': []}
```

### Step 4: Assign pattern_format = value

```python
pattern_format = schema_obj['objects']['formats'][pattern]['pattern']
```

### Step 5: Assign search_pattern = value

```python
search_pattern = '^' + pattern_format + '$'
```

### Step 6: Assign search = re.compile(...)

```python
search = re.compile(search_pattern)
```

### Step 7: Assign pattern_format = value

```python
pattern_format = schema_obj['objects']['formats'][pattern]['pattern']
```

### Step 8: Assign search_pattern = value

```python
search_pattern = f'^{pattern_format}$'
```

### Step 9: Assign search = re.compile(...)

```python
search = re.compile(search_pattern)
```

**Verification:**
```python
assert bool(search.fullmatch(test_string)), f"'{test_string}' is not a valid match for the pattern '{search.pattern}'"
```


## Complete Example

```python
# Setup
# Fixtures: schema_obj

# Workflow
'Test valid string patterns allowed by the specification.'
import re
GOOD_PATTERNS = {'label': ['01', 'test', 'test01', 'Test01'], 'index': ['01', '1', '10000', '00001'], 'string': ['any string is valid.'], 'integer': ['5', '10', '-5', '-10'], 'number': ['5', '3.14', '-5', '-3.14', '1e3', '-2.1E+5'], 'boolean': ['true', 'false'], 'date': ['2022-01-05', '2022-01-05UTC', '2022-50-50'], 'datetime': ['2022-01-05T13:16:30', '2022-01-05T13:16:30.5', '2022-01-05T13:16:30.000005', '2022-01-05T13:16:30Z', '2022-01-05T13:16:30.05Z', '2022-01-05T13:16:30+01:00', '2022-01-05T13:16:30-05:00'], 'time': ['13:16:30', '09:00:00', '9:00:00'], 'unit': ['any string is valid.'], 'file_relative': ['file_in_same_directory.txt', '../../relative/path/file.txt', 'sub-01/path/file.txt'], 'stimuli_relative': ['any/arbitrary/path/file.txt'], 'dataset_relative': ['any/arbitrary/path/file.txt'], 'participant_relative': ['any/arbitrary/path/file.txt'], 'rrid': ['RRID:SCR_017398'], 'uri': ['foo://example.com:8042/over/there?name=ferret#nose'], 'bids_uri': ['bids::sub-01/fmap/sub-01_dir-AP_epi.nii.gz', 'bids:ds000001:sub-02/anat/sub-02_T1w.nii.gz', 'bids:myderivatives:sub-03/func/sub-03_task-rest_space-MNI152_bold.nii.gz']}
for pattern, test_list in GOOD_PATTERNS.items():
    pattern_format = schema_obj['objects']['formats'][pattern]['pattern']
    search_pattern = '^' + pattern_format + '$'
    search = re.compile(search_pattern)
    for test_string in test_list:
        assert bool(search.fullmatch(test_string)), f"'{test_string}' is not a valid match for the pattern '{search.pattern}'"
BAD_PATTERNS = {'label': ['test_01', '!', '010101-', '01-01', '-01'], 'index': ['test', '0.1', '0-1', '0_1'], 'string': [], 'integer': ['3.14', '-3.14', '1.', '-1.', 'string', 's1', '1%', 'one'], 'number': ['string', '1%'], 'boolean': ['True', 'False', 'T', 'F'], 'date': ['05-01-2022', '05/01/2022'], 'datetime': ['2022-01-05T13:16:30.1000005', '2022-01-05T13:16:30U', '2022-01-05T13:16:30UTCUTC', '2022-01-05T34:10:10'], 'time': ['34:10:10', '24:00:00', '00:60:00', '00:00:60', '01:23'], 'unit': [], 'file_relative': ['/path/with/starting/slash/file.txt'], 'stimuli_relative': ['/path/with/starting/slash/file.txt', 'stimuli/path/file.txt'], 'dataset_relative': ['/path/with/starting/slash/file.txt'], 'participant_relative': ['/path/with/starting/slash/file.txt', 'sub-01/path/file.txt'], 'rrid': ['RRID:'], 'uri': [], 'bids_uri': []}
for pattern, test_list in BAD_PATTERNS.items():
    pattern_format = schema_obj['objects']['formats'][pattern]['pattern']
    search_pattern = f'^{pattern_format}$'
    search = re.compile(search_pattern)
    for test_string in test_list:
        assert not bool(search.fullmatch(test_string)), f"'{test_string}' should not be a valid match for the pattern '{search.pattern}'"
```

## Next Steps


---

*Source: test_schema.py:67 | Complexity: Advanced | Last updated: 2026-05-18*