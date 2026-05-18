---
name: bids-specification
description: Local codebase analysis for bids-specification
doc_version: 
---

# bids-specification Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `bids-specification`
**Files Analyzed:** 0
**Languages:** 
**Analysis Depth:** surface

## When to Use This Skill

Use this skill when you need to:
- Understand the codebase architecture and design patterns
- Find implementation examples and usage patterns
- Review API documentation extracted from code
- Check configuration patterns and best practices
- Explore test examples and real-world usage
- Navigate the codebase structure efficiently

## ⚡ Quick Reference

### Codebase Statistics

**Languages:**

**Analysis Performed:**
- ✅ API Reference (C2.5)
- ✅ Dependency Graph (C2.6)
- ✅ Design Patterns (C3.1)
- ✅ Test Examples (C3.2)
- ✅ Configuration Patterns (C3.4)
- ✅ Architectural Analysis (C3.7)
- ✅ Project Documentation (C3.9)

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Instantiate Context: Verify that dataclass values can be assigned to variables annotated with protocols.

For pytest, this just checks instantiability.
Running mypy with bst installed should check assignability,
for example, with::

    uvx --with=. mypy tests** (complexity: 1.00)

```python
context = ctx.Context(schema={}, dataset=dataset, subject=subject, path='path', modality='modality', datatype='datatype', entities={}, suffix='suffix', extension='.ext', size=0, sidecar={}, associations=associations, gzip=gzip, tiff=tiff, ome=ome, nifti_header=nifti_header, columns={}, json={})
```

**Workflow: Verify that dataclass values can be assigned to variables annotated with protocols.

For pytest, this just checks instantiability.
Running mypy with bst installed should check assignability,
for example, with::

    uvx --with=. mypy tests** (complexity: 1.00)

```python
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

**Workflow: A unit test for utils.resolve_metadata_type.** (complexity: 1.00)

```python
'A unit test for utils.resolve_metadata_type.'
base_definition = {'name': 'Term', 'description': 'A description'}
term_definition1 = base_definition.copy()
term_definition1['type'] = 'string'
target_description = '[string](https://www.w3schools.com/js/js_json_datatypes.asp)'
type_description = utils.resolve_metadata_type(term_definition1)
assert target_description == type_description
term_definition1['enum'] = ['n/a']
target_description = '`"n/a"`'
type_description = utils.resolve_metadata_type(term_definition1)
assert target_description == type_description
```

**Workflow: test entity rule** (complexity: 1.00)

```python
rule = Namespace.build({'datatypes': ['anat'], 'entities': {'subject': 'required', 'session': 'optional'}, 'suffixes': ['T1w'], 'extensions': ['.nii']})
nii_rule = rules._entity_rule(rule, schema_obj)
assert nii_rule == {'regex': 'sub-(?P<subject>[0-9a-zA-Z+]+)/(?:ses-(?P<session>[0-9a-zA-Z+]+)/)?(?P<datatype>anat)/(?(subject)sub-(?P=subject)_)(?(session)ses-(?P=session)_)(?P<suffix>T1w)(?P<extension>\\.nii)\\Z', 'mandatory': False}
assert re.match(nii_rule['regex'], 'sub-01/anat/sub-01_T1w.nii')
assert re.match(nii_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/anat/sub-02_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/sub-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/ses-01/anat/sub-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/anat/sub-01_ses-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-02_T1w.nii')
rule = Namespace.build({'datatypes': ['anat', ''], 'entities': {'subject': 'optional', 'session': 'optional'}, 'suffixes': ['T1w'], 'extensions': ['.json']})
json_rule = rules._entity_rule(rule, schema_obj)
assert json_rule == {'regex': '(?:sub-(?P<subject>[0-9a-zA-Z+]+)/)?(?:ses-(?P<session>[0-9a-zA-Z+]+)/)?(?:(?P<datatype>anat)/)?(?(subject)sub-(?P=subject)_)(?(session)ses-(?P=session)_)(?P<suffix>T1w)(?P<extension>\\.json)\\Z', 'mandatory': False}
assert re.match(json_rule['regex'], 'sub-01/anat/sub-01_T1w.json')
assert re.match(json_rule['regex'], 'sub-01/sub-01_T1w.json')
assert re.match(json_rule['regex'], 'T1w.json')
assert re.match(json_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-01_T1w.json')
assert re.match(json_rule['regex'], 'sub-01/ses-01/sub-01_ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/anat/sub-02_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01_T1w.json')
assert not re.match(json_rule['regex'], 'ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/ses-01/anat/sub-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/anat/sub-01_ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/ses-01/ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-02_T1w.json')
```

**Workflow: test write report** (complexity: 1.00)

```python
from bidsschematools.validator import write_report
validation_result = {}
validation_result['schema_tracking'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9a-zA-Z+]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
validation_result['schema_listing'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
validation_result['path_tracking'] = ['/home/chymera/.data2/datalad/000026/noncompliant/sub-EXC022/anat/sub-EXC022_ses-MRI_flip-1_VFA.nii.gz']
validation_result['path_listing'] = ['/home/chymera/.data2/datalad/000026/noncompliant/sub-EXC022/anat/sub-EXC022_ses-MRI_flip-1_VFA.nii.gz']
report_path = tmp_path / 'output_bids_validator_xs_write.log'
write_report(validation_result, report_path=str(report_path))
expected_report_path = load_test_data('expected_bids_validator_xs_write.log')
assert report_path.read_text() == expected_report_path.read_text()
```

**Workflow: test validate bids** (complexity: 1.00)

```python
selected_dir = os.path.join(bids_examples, BIDS_SELECTION[0])
selected_paths = []
for root, dirs, files in os.walk(selected_dir, topdown=False):
    for f in files:
        selected_path = os.path.join(root, f)
        selected_paths.append(selected_path)
result = validate_bids(selected_paths, schema_path=False)
result = validate_bids(selected_paths, report_path=True)
result = validate_bids(selected_paths, report_path=os.path.join(tmp_path, 'test_bids.log'))
assert len(result['path_tracking']) == 0
schema_path = load.readable('schema')
expected_version = schema_path.joinpath('BIDS_VERSION').read_text().rstrip()
assert result['bids_version'] == expected_version
```

**Workflow: test exclude files** (complexity: 1.00)

```python
from bidsschematools.validator import validate_bids
dataset = 'asl003'
dataset_reference = os.path.join(bids_examples, dataset)
tmp_path = str(tmp_path)
shutil.copytree(dataset_reference, tmp_path, dirs_exist_ok=True)
archive_file_name = 'dandiset.yaml'
archive_file_path = os.path.join(tmp_path, archive_file_name)
with open(archive_file_path, 'w') as f:
    f.write(' \n')
result = validate_bids(tmp_path)
assert len(result['path_tracking']) == 1
result = validate_bids(tmp_path, exclude_files=[archive_file_name])
assert len(result['path_tracking']) == 0
```

**Workflow: test dereferencing** (complexity: 1.00)

```python
orig = {'ReferencedObject': {'Property1': 'value1', 'Property2': 'value2'}, 'ReferencingObject': {'$ref': 'ReferencedObject', 'Property2': 'value4'}}
dereffed = schema.dereference(orig)
assert dereffed == {'ReferencedObject': {'Property1': 'value1', 'Property2': 'value2'}, 'ReferencingObject': {'Property1': 'value1', 'Property2': 'value4'}}
orig = {'raw.func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}, 'derived.func': {'$ref': 'raw.func', 'entities': {'$ref': 'raw.func.entities', 'space': 'optional', 'desc': 'optional'}}}
sch = types.Namespace.build(orig)
dereffed = schema.dereference(sch)
assert dereffed == {'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional', 'space': 'optional', 'desc': 'optional'}}}}
orig = {'_DERIV_ENTS': {'space': 'optional', 'desc': 'optional'}, 'raw.func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}, 'derived.func': {'$ref': 'raw.func', 'entities': {'$ref': '_DERIV_ENTS'}}}
sch = types.Namespace.build(orig)
dereffed = schema.dereference(sch)
assert dereffed == {'_DERIV_ENTS': {'space': 'optional', 'desc': 'optional'}, 'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'space': 'optional', 'desc': 'optional'}}}}
orig = {'objects': {'enums': {'left': {'value': 'L'}, 'right': {'value': 'R'}}, 'entities.hemisphere': {'name': 'hemi', 'enum': [{'$ref': 'objects.enums.left.value'}, {'$ref': 'objects.enums.right.value'}]}}}
sch = types.Namespace.build(orig)
dereffed = schema.dereference(sch)
assert dereffed == {'objects': {'enums': {'left': {'value': 'L'}, 'right': {'value': 'R'}}, 'entities': {'hemisphere': {'name': 'hemi', 'enum': ['L', 'R']}}}}
```

**Workflow: test accept non bids dir** (complexity: 0.90)

```python
from bidsschematools.validator import validate_bids
dataset = 'asl003'
dataset_reference = os.path.join(bids_examples, dataset)
tmp_path = str(tmp_path)
shutil.copytree(dataset_reference, tmp_path, dirs_exist_ok=True)
os.remove(os.path.join(tmp_path, 'dataset_description.json'))
with pytest.raises(ValueError, match='None of the files in the input list are part of a BIDS dataset. Aborting.'):
    _ = validate_bids(tmp_path)
result = validate_bids(tmp_path, accept_non_bids_dir=True)
assert len(result['path_tracking']) == 0
```

**Workflow: Test whether files under the schema objects subdirectory correspond to entries, and
that rules are not misloaded as objects.
This may need to be updated for schema hierarchy changes.** (complexity: 0.80)

```python
'\n    Test whether files under the schema objects subdirectory correspond to entries, and\n    that rules are not misloaded as objects.\n    This may need to be updated for schema hierarchy changes.\n    '
object_files = []
for root, dirs, files in os.walk(schema_dir, topdown=False):
    if 'objects' in root:
        for object_file in files:
            object_base, _ = os.path.splitext(object_file)
            object_files.append(object_base)
rule_files = []
for root, dirs, files in os.walk(schema_dir, topdown=False):
    if 'rules' in root:
        for rule_file in files:
            rule_base, _ = os.path.splitext(rule_file)
            rule_files.append(rule_base)
rules_only = list(filter(lambda a: a not in object_files, rule_files))
glossary = text.make_glossary(schema_obj)
for line in glossary.split('\n'):
    if line.startswith('<a name="objects.'):
        assert any((line.startswith(f'<a name="objects.{i}.') for i in object_files))
        assert not any((line.startswith(f'<a name="objects.{i}.') for i in rules_only))
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 142
**Total Settings:** 11178
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 142 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 67
**Categories:** 5

### Overview

- **DECISION-MAKING.md** (`DECISION-MAKING.md`)
- **Maintainers_Guide.md** (`Maintainers_Guide.md`)
- **README.md** (`README.md`)
- **Release_Guideline.md** (`Release_Guideline.md`)
- **Release_Protocol.md** (`Release_Protocol.md`)
- *...and 1 more*

### Contributing

- **CONTRIBUTING.md** (`CONTRIBUTING.md`)

### Other

- **pull_request_template.md** (`.github/pull_request_template.md`)
- **README.md** (`BIDS_logo/README.md`)
- **README.md** (`pdf_build_src/README.md`)
- **README.md** (`pdf_build_src/tests/data/expected/README.md`)
- **README.md** (`pdf_build_src/tests/data/input/README.md`)
- *...and 38 more*

### Specifications

- **magnetic-resonance-imaging-data.md** (`pdf_build_src/tests/data/expected/modality-specific-files/magnetic-resonance-imaging-data.md`)
- **magnetic-resonance-imaging-data.md** (`pdf_build_src/tests/data/input/modality-specific-files/magnetic-resonance-imaging-data.md`)
- **behavioral-experiments.md** (`src/modality-specific-files/behavioral-experiments.md`)
- **electroencephalography.md** (`src/modality-specific-files/electroencephalography.md`)
- **electromyography.md** (`src/modality-specific-files/electromyography.md`)
- *...and 10 more*

### Templates

- **blank.md** (`.github/ISSUE_TEMPLATE/blank.md`)
- **module.rst** (`tools/schemacode/docs/_templates/module.rst`)

*See `references/documentation/` for all project documentation*

## 📚 Available References

This skill includes detailed reference documentation:

- **Dependencies**: `references/dependencies/` - Dependency graph and analysis
- **Patterns**: `references/patterns/` - Detected design patterns
- **Examples**: `references/test_examples/` - Usage examples from tests
- **Configuration**: `references/config_patterns/` - Configuration patterns
- **Documentation**: `references/documentation/` - Project documentation

---

**Generated by Skill Seeker** | Codebase Analyzer with C3.x Analysis
