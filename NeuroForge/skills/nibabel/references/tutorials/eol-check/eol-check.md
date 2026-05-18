# How To: Eol Check

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test eol check

## Prerequisites

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `nifti1`
- `nifti2`
- `testing`


## Step-by-Step Guide

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert_array_equal(hdr['eol_check'], good_eol)
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert_array_equal(fhdr['eol_check'], good_eol)
```

### Step 3: Assign good_eol = value

```python
good_eol = (13, 10, 26, 10)
```

**Verification:**
```python
assert message == 'EOL check all 0; setting EOL check to 13, 10, 26, 10'
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(hdr['eol_check'], good_eol)
```

**Verification:**
```python
assert_array_equal(fhdr['eol_check'], good_eol)
```

### Step 5: Assign unknown = 0

```python
hdr['eol_check'] = 0
```

**Verification:**
```python
assert message == 'EOL check not 0 or 13, 10, 26, 10; data may be corrupted by EOL conversion; setting EOL check to 13, 10, 26, 10'
```

### Step 6: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 20)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(fhdr['eol_check'], good_eol)
```

**Verification:**
```python
assert message == 'EOL check all 0; setting EOL check to 13, 10, 26, 10'
```

### Step 8: Assign unknown = value

```python
hdr['eol_check'] = (13, 10, 0, 10)
```

### Step 9: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 40)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(fhdr['eol_check'], good_eol)
```

**Verification:**
```python
assert message == 'EOL check not 0 or 13, 10, 26, 10; data may be corrupted by EOL conversion; setting EOL check to 13, 10, 26, 10'
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
good_eol = (13, 10, 26, 10)
assert_array_equal(hdr['eol_check'], good_eol)
hdr['eol_check'] = 0
fhdr, message, raiser = self.log_chk(hdr, 20)
assert_array_equal(fhdr['eol_check'], good_eol)
assert message == 'EOL check all 0; setting EOL check to 13, 10, 26, 10'
hdr['eol_check'] = (13, 10, 0, 10)
fhdr, message, raiser = self.log_chk(hdr, 40)
assert_array_equal(fhdr['eol_check'], good_eol)
assert message == 'EOL check not 0 or 13, 10, 26, 10; data may be corrupted by EOL conversion; setting EOL check to 13, 10, 26, 10'
```

## Next Steps


---

*Source: test_nifti2.py:41 | Complexity: Advanced | Last updated: 2026-05-18*