# bids-specification Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Assignability

- Kind: `tutorial`
- Source: `references/tutorials/assignability/assignability.md`
- Note: Workflow: Verify that dataclass values can be assigned to variables annotated with protocols. For pytest, this just checks instantiability. Running mypy with bst installed should check assignability, for example, with:: 

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

## 2. How To: Entity Rule

- Kind: `tutorial`
- Source: `references/tutorials/entity-rule/entity-rule.md`
- Note: Workflow: test entity rule

```python
# Setup
# Fixtures: schema_obj

# Workflow
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

## 3. How To: Formats

- Kind: `tutorial`
- Source: `references/tutorials/formats/formats.md`
- Note: Workflow: Test valid string patterns allowed by the specification.

```python
# Setup
# Fixtures: schema_obj

# Workflow
'Test valid string patterns allowed by the specification.'
import re
GOOD_PATTERNS = {'label': ['01', 'test', 'test01', 'Test01'], 'index': ['01', '1', '10000', '00001'], 'string': ['any string is valid.'], 'integer': ['5', '10', '-5', '-10'], 'number': ['5', '3.14', '-5', '-3.14', '1e3', '-2.1E+5'], 'boolean': ['true', 'false'], 'date': ['2022-01-05', '2022-01-05UTC', '2022-50-50'], 'datetime': ['2022-01-05T13:16:30', '2022-01-05T13:16:30.5', '2022-01-05T13:16:30.000005', '2022-01-05T13:16:30Z', '2022-01-05T13:16:30.05Z', '2022-01-05T13:16:30+01:00', '2022-01-05T13:16:30-05:00'], 'time': ['13:16:30', '09:00:00', '9:00:00'], 'unit': ['any string is valid.'], 'file_relative': ['file_in_same_directory.txt', '../../relative/path/file.txt', 'sub-01/path/file.txt'], 'stimuli_relative': ['any/arbitrary/path/file.txt'], 'dataset_relative': ['any/arbitrary/path/file.txt'], 'participant_relative': ['any/arbitrary/path/file.txt'], 'rrid': ['RRID:SCR_017398'], 'uri': ['foo://example.com:8042/over/there?name=ferret#nose'], 'bids_uri': ['bids::sub-01/fmap/sub-01_dir-AP_epi.nii.gz', 'bids:ds000001:sub-02/anat/sub-02_T1w.nii.gz', 'bids:myderivatives:sub-03/func/sub-03_task-rest_space-MNI152_bold.nii.gz']}
for pattern, test_list in GOOD_PATTERNS.items():
    pattern_format = schema_obj['objects']['formats'][pattern]['pattern']
    search_pattern = '^' + pattern_format + '$'
    search = re.compile(search_pattern)
    for test_string in test_list:
        assert bool(search.fullmatch(test_string)), f"'{test_string}' is not a valid match for the pattern '{search.pattern}'"
BAD_PATTERNS = {'label': ['test_01', '!', '010101-', '01-01', '-01'], 'index': ['test', '0.1', '0-1', '0_1'], 'string': [], 'integer': ['3.14', '-3.14', '1.', '-1.', 'string', 's1', '1%', 'one'], 'number': ['string', '1%'], 'boolean': ['True', 'False', 'T', 'F'], 'date': ['05-01-2022', '05/01/2022'], 'datetime': ['2022-01-05T13:16:30.1000005', '2022-01-05T13:16:30U', '2022-01-05T13:16:30UTCUTC', '2022-01-05T34:10:10'], 'time': ['34:10:10', '24:00:00', '00:60:00', '00:00:60', '01:23'], 'unit': [], 'file_relative': ['/path/with/starting/slash/file.txt'], 'stimuli_relative': ['/path/with/starting/slash/file.txt', 'stimuli/path/file.txt'], 'dataset_relative': ['/path/with/starting/slash/file.txt'], 'participant_relative': ['/path/with/starting/slash/file.txt', 'sub-01/path/file.txt'], 'rrid': ['RRID:'], 'uri': [], 'bids_uri': []}
for pattern, test_list in BAD_PATTERNS.items():
    pattern_format = schema_obj['objects']['formats'][pattern]['pattern']
    search_pattern = f'^{pattern_format}$'
    search = re.compile(search_pattern)
    for test_string in test_list:
        assert not bool(search.fullmatch(test_string)), f"'{test_string}' should not be a valid match for the pattern '{search.pattern}'"
```

## 4. How To: Dereferencing

- Kind: `tutorial`
- Source: `references/tutorials/dereferencing/dereferencing.md`
- Note: Workflow: test dereferencing

```python
# Workflow
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

## 5. How To: Write Report

- Kind: `tutorial`
- Source: `references/tutorials/write-report/write-report.md`
- Note: Workflow: test write report

```python
# Setup
# Fixtures: tmp_path

# Workflow
from bidsschematools.validator import write_report
validation_result = {}
validation_result['schema_tracking'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9a-zA-Z+]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
validation_result['schema_listing'] = [{'regex': '.*?/sub-(?P<subject>[0-9a-zA-Z+]+)/(|ses-(?P<session>[0-9a-zA-Z+]+)/)anat/sub-(?P=subject)(|_ses-(?P=session))(|_acq-(?P<acquisition>[0-9a-zA-Z+]+))(|_ce-(?P<ceagent>[0-9a-zA-Z+]+))(|_rec-(?P<reconstruction>[0-9a-zA-Z+]+))(|_run-(?P<run>[0-9]+))(|_part-(?P<part>(mag|phase|real|imag)))_(T1w|T2w|PDw|T2starw|FLAIR|inplaneT1|inplaneT2|PDT2|angio|T2star)\\.(nii.gz|nii|json)$', 'mandatory': False}]
validation_result['path_tracking'] = ['/path/to/project']
validation_result['path_listing'] = ['/path/to/project']
report_path = tmp_path / 'output_bids_validator_xs_write.log'
write_report(validation_result, report_path=str(report_path))
expected_report_path = load_test_data('expected_bids_validator_xs_write.log')
assert report_path.read_text() == expected_report_path.read_text()
```

## 6. How To: Accept Non Bids Dir

- Kind: `tutorial`
- Source: `references/tutorials/accept-non-bids-dir/accept-non-bids-dir.md`
- Note: Workflow: test accept non bids dir

```python
# Setup
# Fixtures: bids_examples, tmp_path

# Workflow
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

## 7. How To: Make Sidecar Table

- Kind: `tutorial`
- Source: `references/tutorials/make-sidecar-table/make-sidecar-table.md`
- Note: Workflow: Test whether expected metadata fields are present and the requirement level is applied correctly. This should be robust with respect to schema format.

```python
# Setup
# Fixtures: schema_obj

# Workflow
'\n    Test whether expected metadata fields are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '
rendered_table = tables.make_sidecar_table(schema_obj, 'mri.MRISpatialEncoding').split('\n')
assert rendered_table[0].startswith('| **Key name**')
assert rendered_table[1].startswith('|-------------')
fields = schema_obj.rules.sidecars.mri.MRISpatialEncoding.fields
assert len(rendered_table) == len(fields) + 2
for field, render_row in zip(fields, rendered_table[2:]):
    assert render_row.startswith(f'| [{field}](')
    spec = fields[field]
    if isinstance(spec, str):
        level = normalize_requirements(spec)
        level_addendum = ''
        description_addendum = ''
    else:
        level = normalize_requirements(spec['level'])
        level_addendum = normalize_requirements(spec.get('level_addendum', ''))
        description_addendum = spec.get('description_addendum', '')
    assert f'| {level}' in render_row
    assert level_addendum.split('\n')[0] in render_row
    assert description_addendum.split('\n')[0] in render_row
```

## 8. How To: Make Columns Table

- Kind: `tutorial`
- Source: `references/tutorials/make-columns-table/make-columns-table.md`
- Note: Workflow: Test whether expected columns are present and the requirement level is applied correctly. This should be robust with respect to schema format.

```python
# Setup
# Fixtures: schema_obj

# Workflow
'\n    Test whether expected columns are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '
rendered_table = tables.make_columns_table(schema_obj, 'modality_agnostic.Participants').split('\n')
assert rendered_table[0].startswith('| **Column name**')
assert rendered_table[1].startswith('|----------------')
fields = schema_obj.rules.tabular_data.modality_agnostic.Participants.columns
assert len(rendered_table) == len(fields) + 3
for field, render_row in zip(fields, rendered_table[2:-1]):
    assert render_row.startswith(f'| [{field}](')
    spec = fields[field]
    if isinstance(spec, str):
        level = spec
        level_addendum = ''
        description_addendum = ''
    else:
        level = spec['level']
        level_addendum = spec.get('level_addendum', '').replace('required', 'REQUIRED')
        description_addendum = spec.get('description_addendum', '')
    assert level.upper() in render_row
    assert level_addendum.split('\n')[0] in render_row
    assert description_addendum.split('\n')[0] in render_row
```

## 9. How To: Exclude Files

- Kind: `tutorial`
- Source: `references/tutorials/exclude-files/exclude-files.md`
- Note: Workflow: test exclude files

```python
# Setup
# Fixtures: bids_examples, tmp_path

# Workflow
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

## 10. How To: Valid Sidecar Field

- Kind: `tutorial`
- Source: `references/tutorials/valid-sidecar-field/valid-sidecar-field.md`
- Note: Workflow: Check sidecar fields actually exist in the metadata listed in the schema. Test failures are usually due to typos.

```python
# Setup
# Fixtures: schema_obj

# Workflow
'Check sidecar fields actually exist in the metadata listed in the schema.\n\n    Test failures are usually due to typos.\n    '
field_names = {field.name for field in schema_obj.objects.metadata.values()}
column_names = {column.name for column in schema_obj.objects.columns.values()}
field_or_column_names = field_names | column_names
for key, rule in walk_schema(schema_obj.rules, lambda k, v: isinstance(v, Mapping) and v.get('selectors')):
    for expr_type in ('selector', 'check'):
        for expr in rule.get(f'{expr_type}s', []):
            ast = expression.parse_string(expr)[0]
            for name in find_names(ast):
                if name.startswith('json.'):
                    assert name.split('.', 2)[1] in field_names, f'Bad field in {expr_type}: {name} ({key})'
                elif name.startswith('sidecar.'):
                    assert name.split('.', 2)[1] in field_or_column_names, f'Bad field in {expr_type}: {name} ({key})'
```

## 11. How To: Make Glossary

- Kind: `tutorial`
- Source: `references/tutorials/make-glossary/make-glossary.md`
- Note: Workflow: Test whether files under the schema objects subdirectory correspond to entries, and that rules are not misloaded as objects. This may need to be updated for schema hierarchy changes.

```python
# Setup
# Fixtures: schema_obj, schema_dir

# Workflow
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

## 12. How To: Validate Bids

- Kind: `tutorial`
- Source: `references/tutorials/validate-bids/validate-bids.md`
- Note: Workflow: test validate bids

```python
# Setup
# Fixtures: bids_examples, tmp_path

# Workflow
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
