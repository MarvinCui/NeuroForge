# How To: Spm Scale Checks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test spm scale checks

## Prerequisites

**Required Modules:**
- `numpy`
- `spatialimages`
- `spm2analyze`
- `testing`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

### Step 2: Assign unknown = value

```python
hdr['scl_slope'] = np.nan
```

### Step 3: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 30)
```

### Step 4: yield assert_equal(fhdr['scl_slope'], 1)

```python
yield assert_equal(fhdr['scl_slope'], 1)
```

### Step 5: Assign problem_msg = 'no valid scaling in scalefactor (=None) or cal / gl fields; scalefactor assumed 1.0'

```python
problem_msg = 'no valid scaling in scalefactor (=None) or cal / gl fields; scalefactor assumed 1.0'
```

### Step 6: yield assert_equal(message, problem_msg + '; setting scalefactor "scl_slope" to 1')

```python
yield assert_equal(message, problem_msg + '; setting scalefactor "scl_slope" to 1')
```

### Step 7: yield assert_raises(*raiser)

```python
yield assert_raises(*raiser)
```

### Step 8: Assign dxer = value

```python
dxer = self.header_class.diagnose_binaryblock
```

### Step 9: yield assert_equal(dxer(hdr.binaryblock), problem_msg)

```python
yield assert_equal(dxer(hdr.binaryblock), problem_msg)
```

### Step 10: Assign unknown = value

```python
hdr['scl_slope'] = np.inf
```

### Step 11: yield assert_equal(dxer(hdr.binaryblock), problem_msg)

```python
yield assert_equal(dxer(hdr.binaryblock), problem_msg)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
hdr['scl_slope'] = np.nan
fhdr, message, raiser = self.log_chk(hdr, 30)
yield assert_equal(fhdr['scl_slope'], 1)
problem_msg = 'no valid scaling in scalefactor (=None) or cal / gl fields; scalefactor assumed 1.0'
yield assert_equal(message, problem_msg + '; setting scalefactor "scl_slope" to 1')
yield assert_raises(*raiser)
dxer = self.header_class.diagnose_binaryblock
yield assert_equal(dxer(hdr.binaryblock), problem_msg)
hdr['scl_slope'] = np.inf
yield assert_equal(dxer(hdr.binaryblock), problem_msg)
```

## Next Steps


---

*Source: test_spm2analyze.py:24 | Complexity: Advanced | Last updated: 2026-05-18*