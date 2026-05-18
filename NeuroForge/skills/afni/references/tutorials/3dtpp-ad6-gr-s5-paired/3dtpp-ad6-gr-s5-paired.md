# How To: 3Dtpp Ad6 Gr S5 Paired

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dttest pp AD6 gr s5 paired

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `shutil`
- `afni_test_utils`
- `pytest`

**Setup Required:**
```python
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign seta_l = value

```python
seta_l = ['%s "%s[Vrel#0_Coef]"' % (ad6_idlist[i], data.ad6_olsq[i]) for i in range(len(ad6_idlist))]
```

### Step 2: Assign setb_l = value

```python
setb_l = ['%s "%s[Arel#0_Coef]"' % (ad6_idlist[i], data.ad6_olsq[i]) for i in range(len(ad6_idlist))]
```

### Step 3: Assign seta = unknown.join(...)

```python
seta = ' '.join(seta_l)
```

### Step 4: Assign setb = unknown.join(...)

```python
setb = ' '.join(setb_l)
```

### Step 5: Assign cmd = '\n         3dttest++\n             -prefix {data.outdir}/stat.5.ttest\n             -AminusB\n             -setA Vrel {seta}\n             -setB Arel {setb}\n             -paired\n         '

```python
cmd = '\n         3dttest++\n             -prefix {data.outdir}/stat.5.ttest\n             -AminusB\n             -setA Vrel {seta}\n             -setB Arel {setb}\n             -paired\n         '
```

### Step 6: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 7: Assign rc = tools.OutputDiffer(...)

```python
rc = tools.OutputDiffer(data, cmd, merge_error_with_output=True)
```


## Complete Example

```python
# Setup
# Fixtures: data

# Workflow
seta_l = ['%s "%s[Vrel#0_Coef]"' % (ad6_idlist[i], data.ad6_olsq[i]) for i in range(len(ad6_idlist))]
setb_l = ['%s "%s[Arel#0_Coef]"' % (ad6_idlist[i], data.ad6_olsq[i]) for i in range(len(ad6_idlist))]
seta = ' '.join(seta_l)
setb = ' '.join(setb_l)
cmd = '\n         3dttest++\n             -prefix {data.outdir}/stat.5.ttest\n             -AminusB\n             -setA Vrel {seta}\n             -setB Arel {setb}\n             -paired\n         '
cmd = ' '.join(cmd.format(**locals()).split())
rc = tools.OutputDiffer(data, cmd, merge_error_with_output=True)
```

## Next Steps


---

*Source: test_3dttest++.py:25 | Complexity: Intermediate | Last updated: 2026-05-18*