# nibabel Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Rst Table

- Kind: `tutorial`
- Source: `references/tutorials/rst-table/rst-table.md`
- Note: Workflow: test rst table

```python
# Workflow
R, C = (3, 4)
cell_values = np.arange(R * C).reshape((R, C))
assert rst_table(cell_values) == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
assert rst_table(cell_values, ['a', 'b', 'c']) == '+---+--------+--------+--------+--------+\n|   | col[0] | col[1] | col[2] | col[3] |\n+===+========+========+========+========+\n| a |  0.00  |  1.00  |  2.00  |  3.00  |\n| b |  4.00  |  5.00  |  6.00  |  7.00  |\n| c |  8.00  |  9.00  | 10.00  | 11.00  |\n+---+--------+--------+--------+--------+'
with pytest.raises(ValueError):
    rst_table(cell_values, ['a', 'b'])
with pytest.raises(ValueError):
    rst_table(cell_values, ['a', 'b', 'c', 'd'])
assert rst_table(cell_values, None, ['1', '2', '3', '4']) == '+--------+-------+-------+-------+-------+\n|        |   1   |   2   |   3   |   4   |\n+========+=======+=======+=======+=======+\n| row[0] |  0.00 |  1.00 |  2.00 |  3.00 |\n| row[1] |  4.00 |  5.00 |  6.00 |  7.00 |\n| row[2] |  8.00 |  9.00 | 10.00 | 11.00 |\n+--------+-------+-------+-------+-------+'
with pytest.raises(ValueError):
    rst_table(cell_values, None, ['1', '2', '3'])
with pytest.raises(ValueError):
    rst_table(cell_values, None, list('12345'))
assert rst_table(cell_values, title='A title') == '*******\nA title\n*******\n\n+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
assert rst_table(cell_values, val_fmt='{0}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0      | 1      | 2      | 3      |\n| row[1] | 4      | 5      | 6      | 7      |\n| row[2] | 8      | 9      | 10     | 11     |\n+--------+--------+--------+--------+--------+'
cell_values_back = np.arange(R * C)[::-1].reshape((R, C))
cell_3d = np.dstack((cell_values, cell_values_back))
assert rst_table(cell_3d, val_fmt='{0[0]}-{0[1]}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0-11   | 1-10   | 2-9    | 3-8    |\n| row[1] | 4-7    | 5-6    | 6-5    | 7-4    |\n| row[2] | 8-3    | 9-2    | 10-1   | 11-0   |\n+--------+--------+--------+--------+--------+'
formats = dict(down='!', along='_', thick_long='~', cross='%', title_heading='#')
assert rst_table(cell_values, title='A title', format_chars=formats) == '#######\nA title\n#######\n\n%________%________%________%________%________%\n!        ! col[0] ! col[1] ! col[2] ! col[3] !\n%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%\n! row[0] !  0.00  !  1.00  !  2.00  !  3.00  !\n! row[1] !  4.00  !  5.00  !  6.00  !  7.00  !\n! row[2] !  8.00  !  9.00  ! 10.00  ! 11.00  !\n%________%________%________%________%________%'
formats['funny_value'] = '!'
with pytest.raises(ValueError):
    rst_table(cell_values, title='A title', format_chars=formats)
```

## 2. How To: Extend

- Kind: `tutorial`
- Source: `references/tutorials/extend/extend.md`
- Note: Workflow: test extend

```python
# Workflow
total_nb_rows = DATA['tractogram'].streamlines.total_nb_rows
sdict = PerArraySequenceDict(total_nb_rows, DATA['data_per_point'])
list_nb_points = [2, 7, 4]
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:]}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
sdict.extend(sdict2)
assert len(sdict) == len(sdict2)
for k in DATA['tractogram'].data_per_point:
    assert_arrays_equal(sdict[k][:len(DATA['tractogram'])], DATA['tractogram'].data_per_point[k])
    assert_arrays_equal(sdict[k][len(DATA['tractogram']):], new_data[k])
sdict_orig = copy.deepcopy(sdict)
sdict.extend(PerArraySequenceDict())
for k in sdict_orig.keys():
    assert_arrays_equal(sdict[k], sdict_orig[k])
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:], 'other': (7,)}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'other': DATA['fa'][0].shape[1:]}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:] + (3,)}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
```

## 3. How To: Slope Inter Castable

- Kind: `tutorial`
- Source: `references/tutorials/slope-inter-castable/slope-inter-castable.md`
- Note: Workflow: test slope inter castable

```python
# Workflow
for in_dtt in FLOAT_TYPES + IUINT_TYPES:
    for out_dtt in NUMERIC_TYPES:
        for klass in (ArrayWriter, SlopeArrayWriter, SlopeInterArrayWriter):
            arr = np.zeros((5,), dtype=in_dtt)
            klass(arr, out_dtt)
arr = np.array([np.inf, np.nan, -np.inf])
for in_dtt in FLOAT_TYPES:
    for out_dtt in IUINT_TYPES:
        in_arr = arr.astype(in_dtt)
        with pytest.raises(WriterError):
            ArrayWriter(in_arr, out_dtt)
        SlopeArrayWriter(arr.astype(in_dtt), out_dtt)
        SlopeInterArrayWriter(arr.astype(in_dtt), out_dtt)
for in_dtt, out_dtt, arr, slope_only, slope_inter, neither in ((np.float32, np.float32, 1, True, True, True), (np.float64, np.float32, 1, True, True, True), (np.float32, np.complex128, 1, True, True, True), (np.uint32, np.complex128, 1, True, True, True), (np.int64, np.float32, 1, True, True, True), (np.float32, np.int16, 1, True, True, False), (np.complex128, np.float32, 1, False, False, False), (np.complex128, np.int16, 1, False, False, False), (np.uint8, np.int16, 1, True, True, True), (np.uint16, np.int16, 1, True, True, True), (np.uint16, np.int16, 2 ** 16 - 1, True, True, False), (np.uint16, np.int16, (0, 2 ** 16 - 1), True, True, False), (np.uint16, np.uint8, 1, True, True, True), (np.int16, np.uint16, 1, True, True, True), (np.int16, np.uint16, -1, True, True, False), (np.int16, np.uint16, (-1, 1), False, True, False), (np.int8, np.uint16, 1, True, True, True), (np.int8, np.uint16, -1, True, True, False), (np.int8, np.uint16, (-1, 1), False, True, False)):
    data = np.array(arr, dtype=in_dtt)
    if slope_only:
        SlopeArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            SlopeArrayWriter(data, out_dtt)
    if slope_inter:
        SlopeInterArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            SlopeInterArrayWriter(data, out_dtt)
    if neither:
        ArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            ArrayWriter(data, out_dtt)
```

## 4. How To: Image Class

- Kind: `tutorial`
- Source: `references/tutorials/image-class/image-class.md`
- Note: Workflow: Compare an image of one image class to all others. The function should make sure that it loads the image with the expected class, but failing when given a bad sniff (when the sniff is used).

```python
# Setup
# Fixtures: img_path, expected_img_klass

# Workflow
'Compare an image of one image class to all others.\n\n        The function should make sure that it loads the image with the expected\n        class, but failing when given a bad sniff (when the sniff is used).'

def check_img(img_path, img_klass, sniff_mode, sniff, expect_success, msg):
    """Embedded function to do the actual checks expected."""
    if sniff_mode == 'no_sniff':
        is_img, new_sniff = img_klass.path_maybe_image(img_path)
    elif sniff_mode in ('empty', 'irrelevant', 'bad_sniff'):
        is_img, new_sniff = img_klass.path_maybe_image(img_path, (sniff, img_path))
    else:
        is_img, new_sniff = img_klass.path_maybe_image(img_path, sniff)
    if expect_success:
        new_msg = f'{img_klass.__name__} returned sniff==None ({msg})'
        expected_sizeof_hdr = getattr(img_klass.header_class, 'sizeof_hdr', 0)
        current_sizeof_hdr = 0 if new_sniff is None else len(new_sniff[0])
        assert current_sizeof_hdr >= expected_sizeof_hdr, new_msg
        new_msg = f"{basename(img_path)} ({msg}) image is{('' if is_img else ' not')} a {img_klass.__name__} image."
        assert is_img, new_msg
    if sniff_mode == 'vanilla':
        return new_sniff
    else:
        return sniff
sizeof_hdr = getattr(expected_img_klass.header_class, 'sizeof_hdr', 0)
for sniff_mode, sniff in dict(vanilla=None, no_sniff=None, none=None, empty=b'', irrelevant=b'a' * (sizeof_hdr - 1), bad_sniff=b'a' * sizeof_hdr).items():
    for klass in img_klasses:
        if klass == expected_img_klass:
            expect_success = sniff_mode != 'bad_sniff' or sizeof_hdr == 0
        else:
            expect_success = False
        msg = f'{expected_img_klass.__name__}/ {sniff_mode}/ {expect_success}'
        sniff = check_img(img_path, klass, sniff_mode=sniff_mode, sniff=sniff, expect_success=expect_success, msg=msg)
```

## 5. How To: Read Geometry

- Kind: `tutorial`
- Source: `references/tutorials/read-geometry/read-geometry.md`
- Note: Workflow: test read geometry

```python
# Workflow
img = ci.Cifti2Image.from_filename(DATA_FILE6)
geometry_mapping = img.header.matrix.get_index_map(1)
expected_geometry = [('CIFTI_STRUCTURE_CORTEX_LEFT', 29696, 0, 32491), ('CIFTI_STRUCTURE_CORTEX_RIGHT', 29716, 0, 32491), ('CIFTI_STRUCTURE_ACCUMBENS_LEFT', 135, [49, 66, 28], [48, 72, 35]), ('CIFTI_STRUCTURE_ACCUMBENS_RIGHT', 140, [40, 66, 29], [43, 66, 36]), ('CIFTI_STRUCTURE_AMYGDALA_LEFT', 315, [55, 61, 21], [56, 58, 31]), ('CIFTI_STRUCTURE_AMYGDALA_RIGHT', 332, [34, 62, 20], [36, 61, 31]), ('CIFTI_STRUCTURE_BRAIN_STEM', 3472, [42, 41, 0], [46, 50, 36]), ('CIFTI_STRUCTURE_CAUDATE_LEFT', 728, [50, 72, 32], [53, 60, 49]), ('CIFTI_STRUCTURE_CAUDATE_RIGHT', 755, [40, 68, 33], [37, 62, 49]), ('CIFTI_STRUCTURE_CEREBELLUM_LEFT', 8709, [49, 35, 4], [46, 37, 37]), ('CIFTI_STRUCTURE_CEREBELLUM_RIGHT', 9144, [38, 35, 4], [44, 38, 36]), ('CIFTI_STRUCTURE_DIENCEPHALON_VENTRAL_LEFT', 706, [52, 53, 26], [56, 49, 35]), ('CIFTI_STRUCTURE_DIENCEPHALON_VENTRAL_RIGHT', 712, [39, 54, 26], [35, 49, 36]), ('CIFTI_STRUCTURE_HIPPOCAMPUS_LEFT', 764, [55, 60, 21], [54, 44, 39]), ('CIFTI_STRUCTURE_HIPPOCAMPUS_RIGHT', 795, [33, 60, 21], [38, 45, 39]), ('CIFTI_STRUCTURE_PALLIDUM_LEFT', 297, [56, 59, 32], [55, 61, 39]), ('CIFTI_STRUCTURE_PALLIDUM_RIGHT', 260, [36, 62, 32], [35, 62, 39]), ('CIFTI_STRUCTURE_PUTAMEN_LEFT', 1060, [51, 66, 28], [58, 64, 43]), ('CIFTI_STRUCTURE_PUTAMEN_RIGHT', 1010, [34, 66, 29], [31, 62, 43]), ('CIFTI_STRUCTURE_THALAMUS_LEFT', 1288, [55, 47, 33], [52, 53, 46]), ('CIFTI_STRUCTURE_THALAMUS_RIGHT', 1248, [32, 47, 34], [38, 55, 46])]
current_index = 0
for from_file, expected in zip(geometry_mapping.brain_models, expected_geometry):
    assert from_file.model_type in ('CIFTI_MODEL_TYPE_SURFACE', 'CIFTI_MODEL_TYPE_VOXELS')
    assert from_file.brain_structure == expected[0]
    assert from_file.index_offset == current_index
    assert from_file.index_count == expected[1]
    current_index += from_file.index_count
    if from_file.model_type == 'CIFTI_MODEL_TYPE_SURFACE':
        assert from_file.voxel_indices_ijk is None
        assert len(from_file.vertex_indices) == expected[1]
        assert from_file.vertex_indices[0] == expected[2]
        assert from_file.vertex_indices[-1] == expected[3]
        assert from_file.surface_number_of_vertices == 32492
    else:
        assert from_file.vertex_indices is None
        assert from_file.surface_number_of_vertices is None
        assert len(from_file.voxel_indices_ijk) == expected[1]
        assert from_file.voxel_indices_ijk[0] == expected[2]
        assert from_file.voxel_indices_ijk[-1] == expected[3]
assert current_index == img.shape[1]
expected_affine = [[-2, 0, 0, 90], [0, 2, 0, -126], [0, 0, 2, -72], [0, 0, 0, 1]]
expected_dimensions = (91, 109, 91)
assert np.array_equal(geometry_mapping.volume.transformation_matrix_voxel_indices_ijk_to_xyz.matrix, expected_affine)
assert geometry_mapping.volume.volume_dimensions == expected_dimensions
```

## 6. How To: Tractogram Creation

- Kind: `tutorial`
- Source: `references/tutorials/tractogram-creation/tractogram-creation.md`
- Note: Workflow: test tractogram creation

```python
# Workflow
tractogram = Tractogram()
check_tractogram(tractogram)
assert tractogram.affine_to_rasmm is None
tractogram = Tractogram(streamlines=DATA['streamlines'])
check_tractogram(tractogram, DATA['streamlines'])
affine = np.diag([1, 2, 3, 1])
tractogram = Tractogram(affine_to_rasmm=affine)
assert_array_equal(tractogram.affine_to_rasmm, affine)
tractogram = Tractogram(DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
check_tractogram(tractogram, DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
assert is_data_dict(tractogram.data_per_streamline)
assert is_data_dict(tractogram.data_per_point)
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
assert_tractogram_equal(tractogram2, tractogram)
tractogram = LazyTractogram(DATA['streamlines_func'], DATA['data_per_streamline_func'], DATA['data_per_point_func'])
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
wrong_data = [[(1, 0, 0)] * 1, [(0, 1, 0), (0, 1)], [(0, 0, 1)] * 5]
data_per_point = {'wrong_data': wrong_data}
with pytest.raises(ValueError):
    Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
wrong_data = [[(1, 0, 0)] * 1, [(0, 1)] * 2, [(0, 0, 1)] * 5]
data_per_point = {'wrong_data': wrong_data}
with pytest.raises(ValueError):
    Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
```

## 7. How To: Sorting Multiecho Asl

- Kind: `tutorial`
- Source: `references/tutorials/sorting-multiecho-asl/sorting-multiecho-asl.md`
- Note: Workflow: test sorting multiecho ASL

```python
# Workflow
asl_par = pjoin(DATA_PATH, 'ASL_3D_Multiecho.PAR')
with open(asl_par) as fobj:
    asl_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
np.random.shuffle(asl_hdr.image_defs)
sorted_indices = asl_hdr.get_sorted_slice_indices()
sorted_slices = asl_hdr.image_defs['slice number'][sorted_indices]
sorted_echos = asl_hdr.image_defs['echo number'][sorted_indices]
sorted_dynamics = asl_hdr.image_defs['dynamic scan number'][sorted_indices]
sorted_labels = asl_hdr.image_defs['label type'][sorted_indices]
ntotal = len(asl_hdr.image_defs)
nslices = sorted_slices.max()
nechos = sorted_echos.max()
nlabels = sorted_labels.max()
ndynamics = sorted_dynamics.max()
assert nslices == 8
assert nechos == 3
assert nlabels == 2
assert ndynamics == 2
assert_array_equal(np.all(sorted_dynamics[:ntotal // ndynamics] == 1), True)
assert_array_equal(np.all(sorted_dynamics[ntotal // ndynamics:ntotal] == 2), True)
assert_array_equal(np.all(sorted_labels[:nslices * nechos] == 1), True)
assert_array_equal(np.all(sorted_labels[nslices * nechos:2 * nslices * nechos] == 2), True)
assert_array_equal(np.all(sorted_echos[:nslices] == 1), True)
assert_array_equal(np.all(sorted_echos[nslices:2 * nslices] == 2), True)
assert_array_equal(np.all(sorted_echos[2 * nslices:3 * nslices] == 3), True)
assert_array_equal(sorted_slices[:nslices], np.arange(1, nslices + 1))
vol_labels = asl_hdr.get_volume_labels()
assert list(vol_labels.keys()) == ['echo number', 'label type', 'dynamic scan number']
assert_array_equal(vol_labels['dynamic scan number'], [1] * 6 + [2] * 6)
assert_array_equal(vol_labels['label type'], [1] * 3 + [2] * 3 + [1] * 3 + [2] * 3)
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
```

## 8. How To: Opener Various

- Kind: `tutorial`
- Source: `references/tutorials/opener-various/opener-various.md`
- Note: Workflow: test Opener various

```python
# Workflow
message = b'Oh what a giveaway'
bz2_fileno = hasattr(BZ2File, 'fileno')
if HAVE_INDEXED_GZIP:
    import indexed_gzip as igzip
with InTemporaryDirectory():
    sobj = BytesIO()
    files_to_test = ['test.txt', 'test.txt.gz', 'test.txt.bz2', sobj]
    if HAVE_ZSTD:
        files_to_test += ['test.txt.zst']
    for input in files_to_test:
        with Opener(input, 'wb') as fobj:
            fobj.write(message)
            assert fobj.tell() == len(message)
        if input == sobj:
            input.seek(0)
        with Opener(input, 'rb') as fobj:
            message_back = fobj.read()
            assert message == message_back
            if input == sobj:
                with pytest.raises(UnsupportedOperation):
                    fobj.fileno()
            elif input.endswith('.bz2') and (not bz2_fileno):
                with pytest.raises(AttributeError):
                    fobj.fileno()
            elif input.endswith('gz') and HAVE_INDEXED_GZIP and (Version(igzip.__version__) >= Version('0.7.0')):
                with pytest.raises(igzip.NoHandleError):
                    fobj.fileno()
            else:
                assert fobj.fileno() != 0
```

## 9. How To: Nib Tck2Trk

- Kind: `tutorial`
- Source: `references/tutorials/nib-tck2trk/nib-tck2trk.md`
- Note: Workflow: test nib tck2trk

```python
# Workflow
anat = pjoin(DATA_PATH, 'standard.nii.gz')
standard_tck = pjoin(DATA_PATH, 'standard.tck')
with InTemporaryDirectory() as tmpdir:
    shutil.copy(standard_tck, tmpdir)
    standard_trk = pjoin(tmpdir, 'standard.trk')
    standard_tck = pjoin(tmpdir, 'standard.tck')
    cmd = ['nib-tck2trk', standard_tck, anat]
    code, stdout, stderr = run_command(cmd, check_code=False)
    assert code == 2
    assert 'Expecting anatomical image as first argument' in stderr
    cmd = ['nib-tck2trk', anat, standard_tck]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    assert os.path.isfile(standard_trk)
    tck = nib.streamlines.load(standard_tck)
    trk = nib.streamlines.load(standard_trk)
    assert (trk.streamlines.get_data() == tck.streamlines.get_data()).all()
    assert isinstance(trk, nib.streamlines.TrkFile)
    cmd = ['nib-tck2trk', anat, standard_trk]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping non TCK file' in stdout
    cmd = ['nib-tck2trk', anat, standard_tck]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping existing file' in stdout
    cmd = ['nib-tck2trk', '--force', anat, standard_tck, standard_tck]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    tck = nib.streamlines.load(standard_tck)
    trk = nib.streamlines.load(standard_trk)
    assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

## 10. How To: Load Mmap

- Kind: `tutorial`
- Source: `references/tutorials/load-mmap/load-mmap.md`
- Note: Workflow: test load mmap

```python
# Workflow
img_klass = self.image_class
viral_memmap = memmap_after_ufunc()
with InTemporaryDirectory():
    img, fname, has_scaling = self.get_disk_image()
    file_map = img.file_map.copy()
    for func, param1 in ((img_klass.from_filename, fname), (img_klass.load, fname), (top_load, fname), (img_klass.from_file_map, file_map)):
        for mmap, expected_mode in ((None, 'c'), (True, 'c'), ('c', 'c'), ('r', 'r'), (False, None)):
            if has_scaling and (not viral_memmap):
                expected_mode = None
            kwargs = {}
            if mmap is not None:
                kwargs['mmap'] = mmap
            back_img = func(param1, **kwargs)
            back_data = np.asanyarray(back_img.dataobj)
            if expected_mode is None:
                assert not isinstance(back_data, np.memmap), f'Should not be a {img_klass.__name__}'
            else:
                assert isinstance(back_data, np.memmap), f'Not a {img_klass.__name__}'
                if self.check_mmap_mode:
                    assert back_data.mode == expected_mode
            del back_img, back_data
        with pytest.raises(TypeError):
            func(param1, True)
        with pytest.raises(ValueError):
            func(param1, mmap='rw')
        with pytest.raises(ValueError):
            func(param1, mmap='r+')
```

## 11. How To: Nib Trk2Tck

- Kind: `tutorial`
- Source: `references/tutorials/nib-trk2tck/nib-trk2tck.md`
- Note: Workflow: test nib trk2tck

```python
# Workflow
simple_trk = pjoin(DATA_PATH, 'simple.trk')
standard_trk = pjoin(DATA_PATH, 'standard.trk')
with InTemporaryDirectory() as tmpdir:
    shutil.copy(simple_trk, tmpdir)
    shutil.copy(standard_trk, tmpdir)
    simple_trk = pjoin(tmpdir, 'simple.trk')
    standard_trk = pjoin(tmpdir, 'standard.trk')
    simple_tck = pjoin(tmpdir, 'simple.tck')
    standard_tck = pjoin(tmpdir, 'standard.tck')
    cmd = ['nib-trk2tck', simple_trk]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    assert os.path.isfile(simple_tck)
    trk = nib.streamlines.load(simple_trk)
    tck = nib.streamlines.load(simple_tck)
    assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
    assert isinstance(tck, nib.streamlines.TckFile)
    cmd = ['nib-trk2tck', simple_tck]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping non TRK file' in stdout
    cmd = ['nib-trk2tck', simple_trk]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping existing file' in stdout
    cmd = ['nib-trk2tck', '--force', simple_trk, standard_trk]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    trk = nib.streamlines.load(standard_trk)
    tck = nib.streamlines.load(standard_tck)
    assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

## 12. How To: Gifti Round Trip

- Kind: `tutorial`
- Source: `references/tutorials/gifti-round-trip/gifti-round-trip.md`
- Note: Workflow: test gifti round trip

```python
# Workflow
test_data = b'<?xml version="1.0" encoding="UTF-8"?>\n<!DOCTYPE GIFTI SYSTEM "http://www.nitrc.org/frs/download.php/1594/gifti.dtd">\n<GIFTI\nxmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"\nxsi:noNamespaceSchemaLocation="http://www.nitrc.org/frs/download.php/1303/GIFTI_Caret.xsd"\nVersion="1.0"\nNumberOfDataArrays="2">\n<MetaData>\n<MD>\n<Name><![CDATA[date]]></Name>\n<Value><![CDATA[Thu Nov 15 09:05:22 2007]]></Value>\n</MD>\n</MetaData>\n<LabelTable/>\n<DataArray Intent="NIFTI_INTENT_POINTSET"\nDataType="NIFTI_TYPE_FLOAT32"\nArrayIndexingOrder="RowMajorOrder"\nDimensionality="2"\nDim0="4"\nDim1="3"\nEncoding="ASCII"\nEndian="LittleEndian"\nExternalFileName=""\nExternalFileOffset="">\n<CoordinateSystemTransformMatrix>\n<DataSpace><![CDATA[NIFTI_XFORM_TALAIRACH]]></DataSpace>\n<TransformedSpace><![CDATA[NIFTI_XFORM_TALAIRACH]]></TransformedSpace>\n<MatrixData>\n1.000000 0.000000 0.000000 0.000000\n0.000000 1.000000 0.000000 0.000000\n0.000000 0.000000 1.000000 0.000000\n0.000000 0.000000 0.000000 1.000000\n</MatrixData>\n</CoordinateSystemTransformMatrix>\n<Data>\n10.5 0 0\n0 20.5 0\n0 0 30.5\n0 0 0\n</Data>\n</DataArray>\n<DataArray Intent="NIFTI_INTENT_TRIANGLE"\nDataType="NIFTI_TYPE_INT32"\nArrayIndexingOrder="RowMajorOrder"\nDimensionality="2"\nDim0="4"\nDim1="3"\nEncoding="ASCII"\nEndian="LittleEndian"\nExternalFileName="" ExternalFileOffset="">\n<Data>\n0 1 2\n1 2 3\n0 1 3\n0 2 3\n</Data>\n</DataArray>\n</GIFTI>'
exp_verts = np.zeros((4, 3))
exp_verts[0, 0] = 10.5
exp_verts[1, 1] = 20.5
exp_verts[2, 2] = 30.5
exp_faces = np.asarray([[0, 1, 2], [1, 2, 3], [0, 1, 3], [0, 2, 3]], dtype=np.int32)

def _check_gifti(gio):
    vertices = gio.get_arrays_from_intent('NIFTI_INTENT_POINTSET')[0].data
    faces = gio.get_arrays_from_intent('NIFTI_INTENT_TRIANGLE')[0].data
    assert_array_equal(vertices, exp_verts)
    assert_array_equal(faces, exp_faces)
bio = BytesIO()
fmap = dict(image=FileHolder(fileobj=bio))
bio.write(test_data)
bio.seek(0)
gio = GiftiImage.from_file_map(fmap)
_check_gifti(gio)
bio.seek(0)
gio.to_file_map(fmap)
bio.seek(0)
gio2 = GiftiImage.from_file_map(fmap)
_check_gifti(gio2)
```
