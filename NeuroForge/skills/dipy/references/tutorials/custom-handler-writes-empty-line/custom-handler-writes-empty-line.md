# How To: Custom Handler Writes Empty Line

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test custom handler writes empty line

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `logging`
- `dipy.utils.logging`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: Assign stream = io.StringIO(...)

```python
stream = io.StringIO()
```

**Verification:**
```python
assert 'First message' in output
```

### Step 2: Assign handler = CustomHandler(...)

```python
handler = CustomHandler(stream=stream)
```

**Verification:**
```python
assert '\n\n' in output
```

### Step 3: Assign logger = logging.getLogger(...)

```python
logger = logging.getLogger('dipy_custom_handler_test')
```

**Verification:**
```python
assert 'Second message' in output
```

### Step 4: Call logger.handlers.clear()

```python
logger.handlers.clear()
```

### Step 5: Call logger.addHandler()

```python
logger.addHandler(handler)
```

### Step 6: Call logger.setLevel()

```python
logger.setLevel(logging.INFO)
```

### Step 7: Call logger.info()

```python
logger.info('First message')
```

### Step 8: Call logger.info()

```python
logger.info('')
```

### Step 9: Call logger.info()

```python
logger.info('Second message')
```

### Step 10: Call handler.flush()

```python
handler.flush()
```

### Step 11: Assign output = stream.getvalue(...)

```python
output = stream.getvalue()
```

**Verification:**
```python
assert 'First message' in output
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
stream = io.StringIO()
handler = CustomHandler(stream=stream)
logger = logging.getLogger('dipy_custom_handler_test')
logger.handlers.clear()
logger.addHandler(handler)
logger.setLevel(logging.INFO)
logger.info('First message')
logger.info('')
logger.info('Second message')
handler.flush()
output = stream.getvalue()
assert 'First message' in output
assert '\n\n' in output
assert 'Second message' in output
```

## Next Steps


---

*Source: test_logging.py:44 | Complexity: Advanced | Last updated: 2026-05-18*