# How To: Find The Biggest

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test Find the biggest

## Prerequisites

**Required Modules:**
- `os`
- `nipype.interfaces.fsl.dti`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `pytest`
- `nipype.testing.fixtures`


## Step-by-Step Guide

### Step 1: Assign fbg = fsl.FindTheBiggest(...)

```python
fbg = fsl.FindTheBiggest()
```

**Verification:**
```python
assert fbg.cmd == 'find_the_biggest'
```

### Step 2: Assign fbg.inputs.infiles = 'seed*'

```python
fbg.inputs.infiles = 'seed*'
```

**Verification:**
```python
assert fbg.cmdline == 'find_the_biggest seed* fbgfile'
```

### Step 3: Assign fbg.inputs.outfile = 'fbgfile'

```python
fbg.inputs.outfile = 'fbgfile'
```

**Verification:**
```python
assert fbg2.cmdline == 'find_the_biggest seed2* fbgfile2'
```

### Step 4: Assign fbg2 = fsl.FindTheBiggest(...)

```python
fbg2 = fsl.FindTheBiggest(infiles='seed2*', outfile='fbgfile2')
```

**Verification:**
```python
assert results.runtime.cmdline == 'find_the_biggest seed3 out3'
```

### Step 5: Assign fbg3 = fsl.FindTheBiggest(...)

```python
fbg3 = fsl.FindTheBiggest()
```

### Step 6: Assign results = fbg3.run(...)

```python
results = fbg3.run(infiles='seed3', outfile='out3')
```

**Verification:**
```python
assert results.runtime.cmdline == 'find_the_biggest seed3 out3'
```

### Step 7: Call fbg.run()

```python
fbg.run()
```


## Complete Example

```python
# Workflow
fbg = fsl.FindTheBiggest()
assert fbg.cmd == 'find_the_biggest'
with pytest.raises(ValueError):
    fbg.run()
fbg.inputs.infiles = 'seed*'
fbg.inputs.outfile = 'fbgfile'
assert fbg.cmdline == 'find_the_biggest seed* fbgfile'
fbg2 = fsl.FindTheBiggest(infiles='seed2*', outfile='fbgfile2')
assert fbg2.cmdline == 'find_the_biggest seed2* fbgfile2'
fbg3 = fsl.FindTheBiggest()
results = fbg3.run(infiles='seed3', outfile='out3')
assert results.runtime.cmdline == 'find_the_biggest seed3 out3'
```

## Next Steps


---

*Source: test_dti.py:307 | Complexity: Intermediate | Last updated: 2026-05-18*