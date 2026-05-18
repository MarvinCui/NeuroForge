# How To: Bunch Hash

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bunch hash

## Prerequisites

**Required Modules:**
- `os`
- `pytest`
- `acres`
- `utils.filemanip`


## Step-by-Step Guide

### Step 1: Assign json_pth = acres.Loader.cached(...)

```python
json_pth = acres.Loader('nipype.testing').cached('data', 'realign_json.json')
```

**Verification:**
```python
assert bhash == 'd1f46750044c3de102efc847720fc35f'
```

### Step 2: Assign b = nib.Bunch(...)

```python
b = nib.Bunch(infile=str(json_pth), otherthing='blue', yat=True)
```

**Verification:**
```python
assert newbdict['infile'][0][1] == jshash.hexdigest()
```

### Step 3: Assign unknown = b._get_bunch_hash(...)

```python
newbdict, bhash = b._get_bunch_hash()
```

**Verification:**
```python
assert newbdict['yat'] is True
```

### Step 4: Assign jshash = md5(...)

```python
jshash = md5()
```

### Step 5: Call jshash.update()

```python
jshash.update(json_pth.read_bytes())
```

**Verification:**
```python
assert newbdict['infile'][0][1] == jshash.hexdigest()
```


## Complete Example

```python
# Workflow
json_pth = acres.Loader('nipype.testing').cached('data', 'realign_json.json')
b = nib.Bunch(infile=str(json_pth), otherthing='blue', yat=True)
newbdict, bhash = b._get_bunch_hash()
assert bhash == 'd1f46750044c3de102efc847720fc35f'
jshash = md5()
jshash.update(json_pth.read_bytes())
assert newbdict['infile'][0][1] == jshash.hexdigest()
assert newbdict['yat'] is True
```

## Next Steps


---

*Source: test_support.py:42 | Complexity: Intermediate | Last updated: 2026-05-18*