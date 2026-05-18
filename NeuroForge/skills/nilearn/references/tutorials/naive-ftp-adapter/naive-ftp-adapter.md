# How To: Naive Ftp Adapter

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test _NaiveFTPAdapter error.

## Prerequisites

**Required Modules:**
- `gzip`
- `os`
- `re`
- `shutil`
- `tarfile`
- `urllib`
- `pathlib`
- `unittest.mock`
- `zipfile`
- `numpy`
- `pytest`
- `requests`
- `nilearn.datasets`
- `nilearn.datasets.tests.conftest`


## Step-by-Step Guide

### Step 1: 'Test _NaiveFTPAdapter error.'

```python
'Test _NaiveFTPAdapter error.'
```

### Step 2: Assign sender = _utils._NaiveFTPAdapter(...)

```python
sender = _utils._NaiveFTPAdapter()
```

### Step 3: Assign resp = sender.send(...)

```python
resp = sender.send(requests.Request('GET', 'ftp://example.com').prepare())
```

### Step 4: Call resp.close()

```python
resp.close()
```

### Step 5: Call resp.raw.close.assert_called_with()

```python
resp.raw.close.assert_called_with()
```

### Step 6: Assign urllib.request.OpenerDirector.open.side_effect = urllib.error.URLError(...)

```python
urllib.request.OpenerDirector.open.side_effect = urllib.error.URLError('timeout')
```

### Step 7: Assign resp = sender.send(...)

```python
resp = sender.send(requests.Request('GET', 'ftp://example.com').prepare())
```


## Complete Example

```python
# Workflow
'Test _NaiveFTPAdapter error.'
sender = _utils._NaiveFTPAdapter()
resp = sender.send(requests.Request('GET', 'ftp://example.com').prepare())
resp.close()
resp.raw.close.assert_called_with()
urllib.request.OpenerDirector.open.side_effect = urllib.error.URLError('timeout')
with pytest.raises(requests.RequestException, match='timeout'):
    resp = sender.send(requests.Request('GET', 'ftp://example.com').prepare())
```

## Next Steps


---

*Source: test_utils.py:634 | Complexity: Intermediate | Last updated: 2026-05-18*