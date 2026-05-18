# How To: Sender Regex

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test sender regex

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

### Step 1: Assign url = 'https://example.org/info?key=value&name=nilearn'

```python
url = 'https://example.org/info?key=value&name=nilearn'
```

**Verification:**
```python
assert resp.text == 'in info: hello nilearn'
```

### Step 2: Assign pattern = re.compile(...)

```python
pattern = re.compile('.*example.org/(?P<section>.*)\\?.*name=(?P<name>[^&]+)')
```

**Verification:**
```python
assert resp.text == f'name: nilearn, url: {url}'
```

### Step 3: Assign unknown = 'in \\g<section>: hello \\2'

```python
request_mocker.url_mapping[pattern] = 'in \\g<section>: hello \\2'
```

### Step 4: Assign resp = requests.get(...)

```python
resp = requests.get(url)
```

**Verification:**
```python
assert resp.text == 'in info: hello nilearn'
```

### Step 5: Assign unknown = f

```python
request_mocker.url_mapping[pattern] = f
```

### Step 6: Assign resp = requests.get(...)

```python
resp = requests.get(url)
```

**Verification:**
```python
assert resp.text == f'name: nilearn, url: {url}'
```

### Step 7: Assign unknown = g

```python
request_mocker.url_mapping[pattern] = g
```

### Step 8: Assign resp = requests.get(...)

```python
resp = requests.get(url)
```

### Step 9: Call resp.raise_for_status()

```python
resp.raise_for_status()
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker

# Workflow
url = 'https://example.org/info?key=value&name=nilearn'
pattern = re.compile('.*example.org/(?P<section>.*)\\?.*name=(?P<name>[^&]+)')
request_mocker.url_mapping[pattern] = 'in \\g<section>: hello \\2'
resp = requests.get(url)
assert resp.text == 'in info: hello nilearn'

def f(match, request):
    return f"name: {match.group('name')}, url: {request.url}"
request_mocker.url_mapping[pattern] = f
resp = requests.get(url)
assert resp.text == f'name: nilearn, url: {url}'

def g(match, request):
    return 403
request_mocker.url_mapping[pattern] = g
resp = requests.get(url)
with pytest.raises(requests.HTTPError, match='Error'):
    resp.raise_for_status()
```

## Next Steps


---

*Source: test_testing.py:75 | Complexity: Advanced | Last updated: 2026-05-18*