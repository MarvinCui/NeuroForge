# How To: Fetch Neurovault Errors

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test that errors are logged when the server returns an error code.

May "spam" your standard output with requests exceptions,
but that's expected.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: capsys, request_mocker
```

## Step-by-Step Guide

### Step 1: 'Test that errors are logged when the server returns an error code.\n\n    May "spam" your standard output with requests exceptions,\n    but that\'s expected.\n    '

```python
'Test that errors are logged when the server returns an error code.\n\n    May "spam" your standard output with requests exceptions,\n    but that\'s expected.\n    '
```

**Verification:**
```python
assert match is not None
```

### Step 2: Assign unknown = 500

```python
request_mocker.url_mapping['*'] = 500
```

**Verification:**
```python
assert len(data.images) == 0
```

### Step 3: Assign data = neurovault.fetch_neurovault(...)

```python
data = neurovault.fetch_neurovault()
```

### Step 4: Assign captured = capsys.readouterr(...)

```python
captured = capsys.readouterr()
```

### Step 5: Assign match = re.search(...)

```python
match = re.search('500 Error', captured.err)
```

**Verification:**
```python
assert match is not None
```


## Complete Example

```python
# Setup
# Fixtures: capsys, request_mocker

# Workflow
'Test that errors are logged when the server returns an error code.\n\n    May "spam" your standard output with requests exceptions,\n    but that\'s expected.\n    '
request_mocker.url_mapping['*'] = 500
data = neurovault.fetch_neurovault()
captured = capsys.readouterr()
match = re.search('500 Error', captured.err)
assert match is not None
assert len(data.images) == 0
```

## Next Steps


---

*Source: test_neurovault.py:823 | Complexity: Advanced | Last updated: 2026-05-18*