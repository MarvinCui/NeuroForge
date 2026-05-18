# How To: Request Mocking Autoused Requests

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Check the request mocker is autoused.

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `urllib`
- `requests`


## Step-by-Step Guide

### Step 1: 'Check the request mocker is autoused.'

```python
'Check the request mocker is autoused.'
```

**Verification:**
```python
assert requests.sessions.Session.send.__class__.__name__ == 'Sender'
```

### Step 2: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.com')
```

**Verification:**
```python
assert requests.sessions.Session.send.is_mock
```

### Step 3: Assign resp = requests.post(...)

```python
resp = requests.post('https://example.com', data={'key': 'value'})
```

**Verification:**
```python
assert resp.is_mock
```

### Step 4: Assign session = requests.Session(...)

```python
session = requests.Session()
```

**Verification:**
```python
assert resp.is_mock
```

### Step 5: Assign req = requests.Request(...)

```python
req = requests.Request('GET', 'https://example.com')
```

**Verification:**
```python
assert resp.is_mock
```

### Step 6: Assign prepped = session.prepare_request(...)

```python
prepped = session.prepare_request(req)
```

### Step 7: Assign resp = session.send(...)

```python
resp = session.send(prepped)
```

**Verification:**
```python
assert resp.is_mock
```


## Complete Example

```python
# Workflow
'Check the request mocker is autoused.'
assert requests.sessions.Session.send.__class__.__name__ == 'Sender'
assert requests.sessions.Session.send.is_mock
resp = requests.get('https://example.com')
assert resp.is_mock
resp = requests.post('https://example.com', data={'key': 'value'})
assert resp.is_mock
session = requests.Session()
req = requests.Request('GET', 'https://example.com')
prepped = session.prepare_request(req)
resp = session.send(prepped)
assert resp.is_mock
```

## Next Steps


---

*Source: test_mocking_autoused.py:8 | Complexity: Intermediate | Last updated: 2026-05-18*