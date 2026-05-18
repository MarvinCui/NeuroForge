# How To: Sender Response

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test sender response

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

### Step 1: Assign unknown = _MyResponse(...)

```python
request_mocker.url_mapping['*example.org/a'] = _MyResponse('', '')
```

**Verification:**
```python
assert resp.json() == '{"count": 1}'
```

### Step 2: Assign unknown = f

```python
request_mocker.url_mapping['*example.org/b'] = f
```

**Verification:**
```python
assert resp.headers['cookie'] == 'abc'
```

### Step 3: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/a')
```

**Verification:**
```python
assert resp.json() == '{"count": 1}'
```

### Step 4: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/b')
```

**Verification:**
```python
assert resp.headers['cookie'] == 'abc'
```

### Step 5: Assign resp = Response(...)

```python
resp = Response(b'hello', request.url)
```

### Step 6: Assign unknown = 'abc'

```python
resp.headers['cookie'] = 'abc'
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker

# Workflow
request_mocker.url_mapping['*example.org/a'] = _MyResponse('', '')

def f(match, request):
    resp = Response(b'hello', request.url)
    resp.headers['cookie'] = 'abc'
    return resp
request_mocker.url_mapping['*example.org/b'] = f
resp = requests.get('https://example.org/a')
assert resp.json() == '{"count": 1}'
resp = requests.get('https://example.org/b')
assert resp.headers['cookie'] == 'abc'
```

## Next Steps


---

*Source: test_testing.py:144 | Complexity: Intermediate | Last updated: 2026-05-18*