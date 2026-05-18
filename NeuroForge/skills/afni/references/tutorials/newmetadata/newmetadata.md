# How To: Newmetadata

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test newmetadata

## Prerequisites

**Required Modules:**
- `__future__`
- `os.path`
- `numpy`
- `nifti1`
- `tmpdirs`
- `numpy.testing`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign img = gi.GiftiImage(...)

```python
img = gi.GiftiImage()
```

**Verification:**
```python
assert_true('mykey' in myme)
```

### Step 2: Assign attr = gi.GiftiNVPairs(...)

```python
attr = gi.GiftiNVPairs(name='mykey', value='val1')
```

**Verification:**
```python
assert_true('mykey1' in myme)
```

### Step 3: Assign newmeta = gi.GiftiMetaData(...)

```python
newmeta = gi.GiftiMetaData(attr)
```

**Verification:**
```python
assert_false('mykey' in myme)
```

### Step 4: Call img.set_metadata()

```python
img.set_metadata(newmeta)
```

### Step 5: Assign myme = img.meta.get_metadata(...)

```python
myme = img.meta.get_metadata()
```

### Step 6: Call assert_true()

```python
assert_true('mykey' in myme)
```

### Step 7: Assign newmeta = gi.GiftiMetaData.from_dict(...)

```python
newmeta = gi.GiftiMetaData.from_dict({'mykey1': 'val2'})
```

### Step 8: Call img.set_metadata()

```python
img.set_metadata(newmeta)
```

### Step 9: Assign myme = img.meta.get_metadata(...)

```python
myme = img.meta.get_metadata()
```

### Step 10: Call assert_true()

```python
assert_true('mykey1' in myme)
```

### Step 11: Call assert_false()

```python
assert_false('mykey' in myme)
```


## Complete Example

```python
# Workflow
img = gi.GiftiImage()
attr = gi.GiftiNVPairs(name='mykey', value='val1')
newmeta = gi.GiftiMetaData(attr)
img.set_metadata(newmeta)
myme = img.meta.get_metadata()
assert_true('mykey' in myme)
newmeta = gi.GiftiMetaData.from_dict({'mykey1': 'val2'})
img.set_metadata(newmeta)
myme = img.meta.get_metadata()
assert_true('mykey1' in myme)
assert_false('mykey' in myme)
```

## Next Steps


---

*Source: test_giftiio.py:160 | Complexity: Advanced | Last updated: 2026-05-18*