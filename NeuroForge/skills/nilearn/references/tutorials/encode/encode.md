# How To: Encode

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test base64 encoding/decoding for different dtypes.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `base64`
- `numpy`
- `pytest`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.plotting.js_plotting_utils`
- `nilearn.surface`
- `lxml`

**Setup Required:**
```python
# Fixtures: dtype
```

## Step-by-Step Guide

### Step 1: 'Test base64 encoding/decoding for different dtypes.'

```python
'Test base64 encoding/decoding for different dtypes.'
```

**Verification:**
```python
assert np.allclose(decode(encoded, dtype=dtype), b)
```

### Step 2: Assign a = np.arange(...)

```python
a = np.arange(10, dtype=dtype)
```

**Verification:**
```python
assert np.allclose(a, b)
```

### Step 3: Assign encoded = encode(...)

```python
encoded = encode(a)
```

### Step 4: Assign decoded = base64.b64decode(...)

```python
decoded = base64.b64decode(encoded.encode('utf-8'))
```

### Step 5: Assign b = np.frombuffer(...)

```python
b = np.frombuffer(decoded, dtype=dtype)
```

**Verification:**
```python
assert np.allclose(decode(encoded, dtype=dtype), b)
```


## Complete Example

```python
# Setup
# Fixtures: dtype

# Workflow
'Test base64 encoding/decoding for different dtypes.'
a = np.arange(10, dtype=dtype)
encoded = encode(a)
decoded = base64.b64decode(encoded.encode('utf-8'))
b = np.frombuffer(decoded, dtype=dtype)
assert np.allclose(decode(encoded, dtype=dtype), b)
assert np.allclose(a, b)
```

## Next Steps


---

*Source: test_js_plotting_utils.py:17 | Complexity: Intermediate | Last updated: 2026-05-18*