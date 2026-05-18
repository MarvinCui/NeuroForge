# How To: Log Checks

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test log checks

## Prerequisites

**Required Modules:**
- `logging`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `batteryrunners`
- `casting`
- `spatialimages`
- `volumeutils`
- `wrapstruct`


## Step-by-Step Guide

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert fhdr['an_integer'] == 1
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert message == 'an_integer should be 1; set an_integer to 1'
```

### Step 3: Assign unknown = 2

```python
hdr['an_integer'] = 2
```

**Verification:**
```python
assert message == 'a_str should be lower case; set a_str to lower case'
```

### Step 4: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 40)
```

**Verification:**
```python
assert fhdr['an_integer'] == 1
```

### Step 5: Call pytest.raises()

```python
pytest.raises(*raiser)
```

### Step 6: Assign hdr = HC(...)

```python
hdr = HC()
```

### Step 7: Assign unknown = 'Hello'

```python
hdr['a_str'] = 'Hello'
```

### Step 8: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 20)
```

**Verification:**
```python
assert message == 'a_str should be lower case; set a_str to lower case'
```

### Step 9: Call pytest.raises()

```python
pytest.raises(*raiser)
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
hdr['an_integer'] = 2
fhdr, message, raiser = self.log_chk(hdr, 40)
return
assert fhdr['an_integer'] == 1
assert message == 'an_integer should be 1; set an_integer to 1'
pytest.raises(*raiser)
hdr = HC()
hdr['a_str'] = 'Hello'
fhdr, message, raiser = self.log_chk(hdr, 20)
assert message == 'a_str should be lower case; set a_str to lower case'
pytest.raises(*raiser)
```

## Next Steps


---

*Source: test_wrapstruct.py:455 | Complexity: Advanced | Last updated: 2026-05-18*