# How To: Valid Yaml

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Send the codecov YAML file to CodeCov to check that it's valid, meaning we find out in the
test suite if it's invalid rather than finding out when it tries to run.

## Prerequisites

**Required Modules:**
- `requests`
- `pathlib`


## Step-by-Step Guide

### Step 1: "\n    Send the codecov YAML file to CodeCov to check that it's valid, meaning we find out in the\n    test suite if it's invalid rather than finding out when it tries to run.\n    "

```python
"\n    Send the codecov YAML file to CodeCov to check that it's valid, meaning we find out in the\n    test suite if it's invalid rather than finding out when it tries to run.\n    "
```

**Verification:**
```python
assert resp.status_code == 200, f'`codecov.yaml` is invalid or could not be validated. Message received from Codecov:\n{resp.text}'
```

### Step 2: Assign headers = value

```python
headers = {'Content-Type': 'application/x-www-form-urlencoded'}
```

### Step 3: Assign file = value

```python
file = Path(utils.TESTS_PATH).parent.parent / 'codecov.yml'
```

### Step 4: Assign data = open(...)

```python
data = open(str(file), 'rb')
```

**Verification:**
```python
assert resp.status_code == 200, f'`codecov.yaml` is invalid or could not be validated. Message received from Codecov:\n{resp.text}'
```

### Step 5: Assign resp = requests.post(...)

```python
resp = requests.post('https://codecov.io/validate', headers=headers, data=data, timeout=5)
```

### Step 6: Assign resp = value

```python
resp = {}
```

### Step 7: Assign resp.status_code = 400

```python
resp.status_code = 400
```

### Step 8: Assign resp.text = 'Could not connect to Codecov, timed out after 5s'

```python
resp.text = 'Could not connect to Codecov, timed out after 5s'
```


## Complete Example

```python
# Workflow
"\n    Send the codecov YAML file to CodeCov to check that it's valid, meaning we find out in the\n    test suite if it's invalid rather than finding out when it tries to run.\n    "
headers = {'Content-Type': 'application/x-www-form-urlencoded'}
file = Path(utils.TESTS_PATH).parent.parent / 'codecov.yml'
data = open(str(file), 'rb')
try:
    resp = requests.post('https://codecov.io/validate', headers=headers, data=data, timeout=5)
except TimeoutError:
    resp = {}
    resp.status_code = 400
    resp.text = 'Could not connect to Codecov, timed out after 5s'
assert resp.status_code == 200, f'`codecov.yaml` is invalid or could not be validated. Message received from Codecov:\n{resp.text}'
```

## Next Steps


---

*Source: test_codecov.py:6 | Complexity: Advanced | Last updated: 2026-05-18*