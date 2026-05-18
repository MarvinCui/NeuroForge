# How To: Csas0

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test csas0

## Prerequisites

**Required Modules:**
- `os.path`
- `gzip`
- `numpy`
- `nose.tools`
- `numpy.testing`
- `test_dicomwrappers`


## Step-by-Step Guide

### Step 1: Assign csa_info = csa.read(...)

```python
csa_info = csa.read(CSA2_B1000)
```

**Verification:**
```python
assert_equal(csa_info['type'], 2)
```

### Step 2: Assign b_matrix = value

```python
b_matrix = csa_info['tags']['B_matrix']
```

**Verification:**
```python
assert_equal(csa_info['n_tags'], 83)
```

### Step 3: Call assert_equal()

```python
assert_equal(len(b_matrix['items']), 6)
```

**Verification:**
```python
assert_equal(len(tags), 83)
```

### Step 4: Assign b_value = value

```python
b_value = csa_info['tags']['B_value']
```

**Verification:**
```python
assert_equal(n_o_m['items'], [48])
```

### Step 5: Call assert_equal()

```python
assert_equal(b_value['items'], [1000])
```

**Verification:**
```python
assert_equal(len(b_matrix['items']), 6)
```

### Step 6: Assign csa_info = csa.read(...)

```python
csa_info = csa.read(csa_str)
```

**Verification:**
```python
assert_equal(b_value['items'], [1000])
```

### Step 7: Call assert_equal()

```python
assert_equal(csa_info['type'], 2)
```

### Step 8: Call assert_equal()

```python
assert_equal(csa_info['n_tags'], 83)
```

### Step 9: Assign tags = value

```python
tags = csa_info['tags']
```

### Step 10: Call assert_equal()

```python
assert_equal(len(tags), 83)
```

### Step 11: Assign n_o_m = value

```python
n_o_m = tags['NumberOfImagesInMosaic']
```

### Step 12: Call assert_equal()

```python
assert_equal(n_o_m['items'], [48])
```


## Complete Example

```python
# Workflow
for csa_str in (CSA2_B0, CSA2_B1000):
    csa_info = csa.read(csa_str)
    assert_equal(csa_info['type'], 2)
    assert_equal(csa_info['n_tags'], 83)
    tags = csa_info['tags']
    assert_equal(len(tags), 83)
    n_o_m = tags['NumberOfImagesInMosaic']
    assert_equal(n_o_m['items'], [48])
csa_info = csa.read(CSA2_B1000)
b_matrix = csa_info['tags']['B_matrix']
assert_equal(len(b_matrix['items']), 6)
b_value = csa_info['tags']['B_value']
assert_equal(b_value['items'], [1000])
```

## Next Steps


---

*Source: test_csareader.py:33 | Complexity: Advanced | Last updated: 2026-05-18*