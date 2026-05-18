# How To: Sender Key Order

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test sender key order

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

### Step 1: Assign unknown = 'message'

```python
request_mocker.url_mapping['*message.txt'] = 'message'
```

**Verification:**
```python
assert resp.text == 'message'
```

### Step 2: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/message.txt')
```

**Verification:**
```python
assert resp.text == 'new message'
```

### Step 3: Assign unknown = 'new message'

```python
request_mocker.url_mapping['*.txt'] = 'new message'
```

**Verification:**
```python
assert resp.text == 'new message'
```

### Step 4: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/message.txt')
```

**Verification:**
```python
assert resp.text == 'new message'
```

### Step 5: Assign unknown = 'other message'

```python
request_mocker.url_mapping['*.csv'] = 'other message'
```

### Step 6: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/message.txt')
```

**Verification:**
```python
assert resp.text == 'new message'
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker

# Workflow
request_mocker.url_mapping['*message.txt'] = 'message'
resp = requests.get('https://example.org/message.txt')
assert resp.text == 'message'
request_mocker.url_mapping['*.txt'] = 'new message'
resp = requests.get('https://example.org/message.txt')
assert resp.text == 'new message'
request_mocker.url_mapping['*.csv'] = 'other message'
resp = requests.get('https://example.org/message.txt')
assert resp.text == 'new message'
```

## Next Steps


---

*Source: test_testing.py:15 | Complexity: Intermediate | Last updated: 2026-05-18*