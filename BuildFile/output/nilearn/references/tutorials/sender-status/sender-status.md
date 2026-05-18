# How To: Sender Status

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test sender status

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `tarfile`
- `zipfile`
- `pathlib`
- `pytest`
- `requests`
- `nilearn`
- `nilearn._utils.data_gen`
- `nilearn.datasets.tests._testing`
- `nilearn.datasets.tests.conftest`

**Setup Required:**
```python
# Fixtures: request_mocker
```

## Step-by-Step Guide

### Step 1: Assign unknown = 200

```python
request_mocker.url_mapping['*good'] = 200
```

**Verification:**
```python
assert resp.status_code == 200
```

### Step 2: Assign unknown = 403

```python
request_mocker.url_mapping['*forbidden'] = 403
```

**Verification:**
```python
assert resp.text == 'OK'
```

### Step 3: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/good')
```

**Verification:**
```python
assert resp.status_code == 403
```

### Step 4: Call resp.raise_for_status()

```python
resp.raise_for_status()
```

**Verification:**
```python
assert resp.text == 'ERROR'
```

### Step 5: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/forbidden')
```

**Verification:**
```python
assert resp.status_code == 403
```

### Step 6: Call resp.raise_for_status()

```python
resp.raise_for_status()
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker

# Workflow
request_mocker.url_mapping['*good'] = 200
request_mocker.url_mapping['*forbidden'] = 403
resp = requests.get('https://example.org/good')
assert resp.status_code == 200
assert resp.text == 'OK'
resp.raise_for_status()
resp = requests.get('https://example.org/forbidden')
assert resp.status_code == 403
assert resp.text == 'ERROR'
with pytest.raises(requests.HTTPError, match='Error'):
    resp.raise_for_status()
```

## Next Steps


---

*Source: test_testing.py:102 | Complexity: Intermediate | Last updated: 2026-05-18*