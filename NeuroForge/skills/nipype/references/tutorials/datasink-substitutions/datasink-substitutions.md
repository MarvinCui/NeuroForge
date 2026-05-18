# How To: Datasink Substitutions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test datasink substitutions

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `simplejson`
- `glob`
- `os.path`
- `subprocess`
- `hashlib`
- `collections`
- `pytest`
- `nipype`
- `nipype.interfaces.io`
- `nipype.interfaces.base.traits_extension`
- `nipype.interfaces.base`
- `nipype.utils.filemanip`
- `subprocess`
- `boto`
- `boto.s3.connection`
- `boto3`
- `botocore.utils`
- `paramiko`
- `bids`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign indir = tmpdir.mkdir(...)

```python
indir = tmpdir.mkdir('-Tmp-nipype_ds_subs_in')
```

**Verification:**
```python
assert sorted([os.path.basename(x) for x in glob.glob(os.path.join(str(outdir), '*'))]) == ['!-yz-b.n', 'ABABAB.n']
```

### Step 2: Assign outdir = tmpdir.mkdir(...)

```python
outdir = tmpdir.mkdir('-Tmp-nipype_ds_subs_out')
```

### Step 3: Assign files = value

```python
files = []
```

### Step 4: Assign ds = nio.DataSink(...)

```python
ds = nio.DataSink(parameterization=False, base_directory=str(outdir), substitutions=[('ababab', 'ABABAB')], regexp_substitutions=[('xABABAB(\\w*)\\.n$', 'a-\\1-b.n'), ('(.*%s)[-a]([^%s]*)$' % ((os.path.sep,) * 2), '\\1!\\2')])
```

### Step 5: Call setattr()

```python
setattr(ds.inputs, '@outdir', files)
```

### Step 6: Call ds.run()

```python
ds.run()
```

**Verification:**
```python
assert sorted([os.path.basename(x) for x in glob.glob(os.path.join(str(outdir), '*'))]) == ['!-yz-b.n', 'ABABAB.n']
```

### Step 7: Assign f = str(...)

```python
f = str(indir.join(n))
```

### Step 8: Call files.append()

```python
files.append(f)
```

### Step 9: Call open()

```python
open(f, 'w')
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
indir = tmpdir.mkdir('-Tmp-nipype_ds_subs_in')
outdir = tmpdir.mkdir('-Tmp-nipype_ds_subs_out')
files = []
for n in ['ababab.n', 'xabababyz.n']:
    f = str(indir.join(n))
    files.append(f)
    open(f, 'w')
ds = nio.DataSink(parameterization=False, base_directory=str(outdir), substitutions=[('ababab', 'ABABAB')], regexp_substitutions=[('xABABAB(\\w*)\\.n$', 'a-\\1-b.n'), ('(.*%s)[-a]([^%s]*)$' % ((os.path.sep,) * 2), '\\1!\\2')])
setattr(ds.inputs, '@outdir', files)
ds.run()
assert sorted([os.path.basename(x) for x in glob.glob(os.path.join(str(outdir), '*'))]) == ['!-yz-b.n', 'ABABAB.n']
```

## Next Steps


---

*Source: test_io.py:458 | Complexity: Advanced | Last updated: 2026-05-18*