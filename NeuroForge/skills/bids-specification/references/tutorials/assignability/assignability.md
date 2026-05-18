# How To: Assignability

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Verify that dataclass values can be assigned to variables annotated with protocols.

For pytest, this just checks instantiability.
Running mypy with bst installed should check assignability,
for example, with::

    uvx --with=. mypy tests

## Prerequisites

**Required Modules:**
- `bidsschematools.types`
- `bidsschematools.types`


## Step-by-Step Guide

### Step 1: 'Verify that dataclass values can be assigned to variables annotated with protocols.\n\n    For pytest, this just checks instantiability.\n    Running mypy with bst installed should check assignability,\n    for example, with::\n\n        uvx --with=. mypy tests\n    '

```python
'Verify that dataclass values can be assigned to variables annotated with protocols.\n\n    For pytest, this just checks instantiability.\n    Running mypy with bst installed should check assignability,\n    for example, with::\n\n        uvx --with=. mypy tests\n    '
```

**Verification:**
```python
assert context.schema == {}
```

### Step 2: Assign subjects = ctx.Subjects(...)

```python
subjects = ctx.Subjects([], [])
```

### Step 3: Assign channels = ctx.Channels(...)

```python
channels = ctx.Channels('path', ['TYPE'], ['1'], ['SHORT'])
```

### Step 4: Assign associations = ctx.Associations(...)

```python
associations = ctx.Associations(magnitude=magnitude, magnitude1=magnitude1, m0scan=m0scan, bval=bval, channels=channels, events=events, bvec=bvec, coordsystem=coordsystem, aslcontext=aslcontext)
```

### Step 5: Assign gzip = ctx.Gzip(...)

```python
gzip = ctx.Gzip(0, 'filename', 'comment')
```

### Step 6: Assign sessions = ctx.Sessions(...)

```python
sessions = ctx.Sessions([], [])
```

### Step 7: Assign ome = ctx.Ome(...)

```python
ome = ctx.Ome(PhysicalSizeX=10, PhysicalSizeY=10, PhysicalSizeZ=10, PhysicalSizeXUnit='um', PhysicalSizeYUnit='um', PhysicalSizeZUnit='um')
```

### Step 8: Assign context = ctx.Context(...)

```python
context = ctx.Context(schema={}, dataset=dataset, subject=subject, path='path', modality='modality', datatype='datatype', entities={}, suffix='suffix', extension='.ext', size=0, sidecar={}, associations=associations, gzip=gzip, tiff=tiff, ome=ome, nifti_header=nifti_header, columns={}, json={})
```

**Verification:**
```python
assert context.schema == {}
```


## Complete Example

```python
# Workflow
'Verify that dataclass values can be assigned to variables annotated with protocols.\n\n    For pytest, this just checks instantiability.\n    Running mypy with bst installed should check assignability,\n    for example, with::\n\n        uvx --with=. mypy tests\n    '
subjects: p.Subjects = ctx.Subjects([])
subjects = ctx.Subjects([], [])
dataset: p.Dataset = ctx.Dataset(dataset_description={}, tree={}, ignored=[], datatypes=[], modalities=[], subjects=subjects)
magnitude: p.Magnitude = ctx.Magnitude('path')
magnitude1: p.Magnitude1 = ctx.Magnitude1('path')
m0scan: p.M0scan = ctx.M0scan('path')
bval: p.Bval = ctx.Bval('path', 5, 1, [0, 0, 0, 0, 0])
channels: p.Channels = ctx.Channels('path')
channels = ctx.Channels('path', ['TYPE'], ['1'], ['SHORT'])
events: p.Events = ctx.Events('path', ['0.0', '3.0'])
bvec: p.Bvec = ctx.Bvec('path', 5, 3)
coordsystem: p.Coordsystem = ctx.Coordsystem('path')
aslcontext: p.Aslcontext = ctx.Aslcontext('path', 2, ['label', 'control'])
associations: p.Associations = ctx.Associations()
associations = ctx.Associations(magnitude=magnitude, magnitude1=magnitude1, m0scan=m0scan, bval=bval, channels=channels, events=events, bvec=bvec, coordsystem=coordsystem, aslcontext=aslcontext)
gzip: p.Gzip = ctx.Gzip(0)
gzip = ctx.Gzip(0, 'filename', 'comment')
sessions: p.Sessions = ctx.Sessions([])
sessions = ctx.Sessions([], [])
subject: p.Subject = ctx.Subject(sessions)
tiff: p.Tiff = ctx.Tiff(19789)
dim_info: p.DimInfo = ctx.DimInfo(1, 2, 3)
xyzt_units: p.XyztUnits = ctx.XyztUnits('mm', 'sec')
nifti_header: p.NiftiHeader = ctx.NiftiHeader(dim_info=dim_info, dim=[4, 64, 64, 48, 100, 1, 1, 1], pixdim=[1.0, 1.0, 1.0, 1.0, 1.5, 1.0, 1.0, 1.0], shape=(64, 64, 48, 100), voxel_sizes=(1.0, 1.0, 1.0, 1.5), xyzt_units=xyzt_units, qform_code=1, sform_code=1, axis_codes=('L', 'P', 'S'))
ome: p.Ome = ctx.Ome()
ome = ctx.Ome(PhysicalSizeX=10, PhysicalSizeY=10, PhysicalSizeZ=10, PhysicalSizeXUnit='um', PhysicalSizeYUnit='um', PhysicalSizeZUnit='um')
context: p.Context = ctx.Context(schema={}, dataset=dataset, path='path', size=0, sidecar={}, associations=associations)
context = ctx.Context(schema={}, dataset=dataset, subject=subject, path='path', modality='modality', datatype='datatype', entities={}, suffix='suffix', extension='.ext', size=0, sidecar={}, associations=associations, gzip=gzip, tiff=tiff, ome=ome, nifti_header=nifti_header, columns={}, json={})
assert context.schema == {}
```

## Next Steps


---

*Source: test_context_types.py:14 | Complexity: Advanced | Last updated: 2026-05-18*