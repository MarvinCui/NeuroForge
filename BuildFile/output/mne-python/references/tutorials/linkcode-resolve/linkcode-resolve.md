# How To: Linkcode Resolve

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test linkcode resolving.

## Prerequisites

**Required Modules:**
- `webbrowser`
- `pytest`
- `mne`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test linkcode resolving.'

```python
'Test linkcode resolving.'
```

**Verification:**
```python
assert '/mne/epochs.py' + ex in url
```

### Step 2: Assign ex = '#L'

```python
ex = '#L'
```

**Verification:**
```python
assert '/mne/cov.py' + ex in url
```

### Step 3: Assign url = linkcode_resolve(...)

```python
url = linkcode_resolve('py', dict(module='mne', fullname='Epochs'))
```

**Verification:**
```python
assert '/mne/forward/forward.py' + ex in url
```

### Step 4: Assign url = linkcode_resolve(...)

```python
url = linkcode_resolve('py', dict(module='mne', fullname='compute_covariance'))
```

**Verification:**
```python
assert '/mne/datasets/sample/sample.py' + ex in url
```

### Step 5: Assign url = linkcode_resolve(...)

```python
url = linkcode_resolve('py', dict(module='mne', fullname='convert_forward_solution'))
```

**Verification:**
```python
assert '/mne/forward/forward.py' + ex in url
```

### Step 6: Assign url = linkcode_resolve(...)

```python
url = linkcode_resolve('py', dict(module='mne', fullname='datasets.sample.data_path'))
```

**Verification:**
```python
assert '/mne/datasets/sample/sample.py' + ex in url
```


## Complete Example

```python
# Workflow
'Test linkcode resolving.'
ex = '#L'
url = linkcode_resolve('py', dict(module='mne', fullname='Epochs'))
assert '/mne/epochs.py' + ex in url
url = linkcode_resolve('py', dict(module='mne', fullname='compute_covariance'))
assert '/mne/cov.py' + ex in url
url = linkcode_resolve('py', dict(module='mne', fullname='convert_forward_solution'))
assert '/mne/forward/forward.py' + ex in url
url = linkcode_resolve('py', dict(module='mne', fullname='datasets.sample.data_path'))
assert '/mne/datasets/sample/sample.py' + ex in url
```

## Next Steps


---

*Source: test_docs.py:246 | Complexity: Intermediate | Last updated: 2026-05-18*