# How To: Save Load Resultfile

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test minimally the save/load functions for result files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `shutil`
- `numpy`

**Setup Required:**
```python
# Fixtures: tmpdir, use_relative
```

## Step-by-Step Guide

### Step 1: 'Test minimally the save/load functions for result files.'

```python
'Test minimally the save/load functions for result files.'
```

**Verification:**
```python
assert result.runtime.dictcopy() == loaded_result.runtime.dictcopy()
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert result.inputs == loaded_result.inputs
```

### Step 3: Assign old_use_relative = config.getboolean(...)

```python
old_use_relative = config.getboolean('execution', 'use_relative_paths')
```

**Verification:**
```python
assert result.outputs.get() == loaded_result.outputs.get()
```

### Step 4: Call config.set()

```python
config.set('execution', 'use_relative_paths', use_relative)
```

**Verification:**
```python
assert result.runtime.dictcopy() == loaded_result2.runtime.dictcopy()
```

### Step 5: Assign spc = pe.Node(...)

```python
spc = pe.Node(StrPathConfuser(in_str='2'), name='spc')
```

**Verification:**
```python
assert result.inputs == loaded_result2.inputs
```

### Step 6: Assign spc.base_dir = value

```python
spc.base_dir = tmpdir.mkdir('node').strpath
```

**Verification:**
```python
assert loaded_result2.outputs.get() != result.outputs.get()
```

### Step 7: Assign result = spc.run(...)

```python
result = spc.run()
```

**Verification:**
```python
assert loaded_result2.outputs.out_path == newpath
```

### Step 8: Assign loaded_result = load_resultfile(...)

```python
loaded_result = load_resultfile(tmpdir.join('node').join('spc').join('result_spc.pklz').strpath)
```

**Verification:**
```python
assert loaded_result2.outputs.out_tuple[0] == newpath
```

### Step 9: Call copytree()

```python
copytree(tmpdir.join('node').strpath, tmpdir.join('node2').strpath)
```

**Verification:**
```python
assert loaded_result2.outputs.out_dict_path['2'] == newpath
```

### Step 10: Call rmtree()

```python
rmtree(tmpdir.join('node').strpath)
```

### Step 11: Call config.set()

```python
config.set('execution', 'use_relative_paths', old_use_relative)
```

### Step 12: Assign loaded_result2 = load_resultfile(...)

```python
loaded_result2 = load_resultfile(tmpdir.join('node2').join('spc').join('result_spc.pklz').strpath)
```

**Verification:**
```python
assert result.runtime.dictcopy() == loaded_result2.runtime.dictcopy()
```

### Step 13: Assign newpath = result.outputs.out_path.replace(...)

```python
newpath = result.outputs.out_path.replace('/node/', '/node2/')
```

**Verification:**
```python
assert loaded_result2.outputs.out_path == newpath
```

### Step 14: Call load_resultfile()

```python
load_resultfile(tmpdir.join('node2').join('spc').join('result_spc.pklz').strpath)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, use_relative

# Workflow
'Test minimally the save/load functions for result files.'
from shutil import copytree, rmtree
tmpdir.chdir()
old_use_relative = config.getboolean('execution', 'use_relative_paths')
config.set('execution', 'use_relative_paths', use_relative)
spc = pe.Node(StrPathConfuser(in_str='2'), name='spc')
spc.base_dir = tmpdir.mkdir('node').strpath
result = spc.run()
loaded_result = load_resultfile(tmpdir.join('node').join('spc').join('result_spc.pklz').strpath)
assert result.runtime.dictcopy() == loaded_result.runtime.dictcopy()
assert result.inputs == loaded_result.inputs
assert result.outputs.get() == loaded_result.outputs.get()
copytree(tmpdir.join('node').strpath, tmpdir.join('node2').strpath)
rmtree(tmpdir.join('node').strpath)
if use_relative:
    loaded_result2 = load_resultfile(tmpdir.join('node2').join('spc').join('result_spc.pklz').strpath)
    assert result.runtime.dictcopy() == loaded_result2.runtime.dictcopy()
    assert result.inputs == loaded_result2.inputs
    assert loaded_result2.outputs.get() != result.outputs.get()
    newpath = result.outputs.out_path.replace('/node/', '/node2/')
    assert loaded_result2.outputs.out_path == newpath
    assert loaded_result2.outputs.out_tuple[0] == newpath
    assert loaded_result2.outputs.out_dict_path['2'] == newpath
else:
    with pytest.raises(nib.TraitError):
        load_resultfile(tmpdir.join('node2').join('spc').join('result_spc.pklz').strpath)
config.set('execution', 'use_relative_paths', old_use_relative)
```

## Next Steps


---

*Source: test_utils.py:289 | Complexity: Advanced | Last updated: 2026-05-18*