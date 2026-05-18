# How To: Pixdim Log Checks

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test pixdim log checks

## Prerequisites

**Required Modules:**
- `os.path`
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `packaging.version`
- `nibabel`
- `nibabel`
- `nibabel.cifti2.parse_cifti2`
- `nibabel.tests`
- `nibabel.tests.nibabel_data`
- `nibabel.tmpdirs`


## Step-by-Step Guide

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert fhdr['pixdim'][1] == 2
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert message == self._pixdim_message + '; setting to abs of pixdim values'
```

### Step 3: Assign unknown = value

```python
hdr['pixdim'][1] = -2
```

**Verification:**
```python
assert raiser == ()
```

### Step 4: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 35)
```

**Verification:**
```python
assert fhdr['pixdim'][1] == 2
```

### Step 5: Call pytest.raises()

```python
pytest.raises(*raiser)
```

### Step 6: Assign hdr = HC(...)

```python
hdr = HC()
```

### Step 7: Assign unknown = 0

```python
hdr['pixdim'][1:4] = 0
```

### Step 8: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 0)
```

**Verification:**
```python
assert raiser == ()
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
hdr['pixdim'][1] = -2
fhdr, message, raiser = self.log_chk(hdr, 35)
assert fhdr['pixdim'][1] == 2
assert message == self._pixdim_message + '; setting to abs of pixdim values'
pytest.raises(*raiser)
hdr = HC()
hdr['pixdim'][1:4] = 0
fhdr, message, raiser = self.log_chk(hdr, 0)
assert raiser == ()
```

## Next Steps


---

*Source: test_cifti2io_header.py:445 | Complexity: Advanced | Last updated: 2026-05-18*